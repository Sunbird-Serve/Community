# MCP Server

#### The Key Design Principle

```
MCP Server acts as a smart middle layer

  Serve Registry          MCP DB             AI Agent
  (permanent home)        (working copy)     (conversational)
        │                       │                   │
        │  pre-fetch at start   │                   │
        │──────────────────────►│  fast reads ──────►│
        │                       │◄── fast writes ───│
        │  sync at end only     │                   │
        │◄──────────────────────│                   │
        │                       │                   │

Result: AI gets instant responses. Serve Registry only called
        at session START (fetch) and END (write-back).
        Nothing is lost between sessions because memory_summaries
        and the session state are all in the MCP DB.
```

That's the complete picture. The MCP server is a stateful middleware, it remembers who the user is, what stage they're at, what they've already said, and it only calls the real Serve platform when it absolutely has to (at the start or end of a session, or when submitting something final like a need).

```
┌─────────────────────────────┐     ┌─────────────────────────────┐
│      SERVE REGISTRY /        │     │       MCP SERVER DB          │
│      SERVE DATABASE          │     │      (AI Conversation Layer) │
│                              │     │                              │
│  Owned by the main           │     │  Owned by the AI/Agent       │
│  Serve application           │     │  layer only                  │
│                              │     │                              │
│  • Volunteer profiles        │     │  • Sessions (state machine)  │
│  • Coordinators              │     │  • Conversation messages     │
│  • Schools                   │     │  • Memory summaries          │
│  • Needs / Need lifecycle    │     │  • Telemetry / audit trail   │
└─────────────────────────────┘     └─────────────────────────────┘
          ▲                                      │
          │  MCP server READ              │
          │  from here (lookup_actor,            │
          │  fetch school, fetch need)           │
          └──────────────────────────────────────┘
          MCP server WRITE back here
          (save profile fields after onboarding,
           submit need, update need status)
```



```
┌──────────────────────────────────────────────────────────┐
│                  WHO TALKS TO WHOM                       │
│                                                          │
│   User (WhatsApp / Web / API)                            │
│          │                                               │
│          ▼                                               │
│   ┌─────────────────┐                                    │
│   │  AI Agent (LLM) │  ◄── reads Prompts from MCP        │
│   │  (Claude etc.)  │                                    │
│   └────────┬────────┘                                    │
│            │  calls Tools                                │
│            ▼                                             │
│   ┌─────────────────────┐                                │
│   │   MCP SERVER        │                                │
│   │                     │                                │
│   └──────┬──────────────┘                                │
│          │                                               │
│    ┌─────┴──────┐                                        │
│    ▼            ▼                                        │
│  DB    Serve Platform APIs                           │
│ (Postgres) (Volunteering + Need)                         │
└──────────────────────────────────────────────────────────┘
```

The AI agent doesn't directly touch any database or API, it only calls MCP tools. The MCP server handles everything else.

#### What's Inside the MCP Server

```
┌─────────────────────────────────────────────────────────────────┐
│                        MCP SERVER                               │
│                                                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────┐   │
│  │ PROMPTS  │  │  TOOLS   │  │SERVICES  │  │  SCHEMAS     │   │
│  │          │  │          │  │          │  │  (Pydantic)  │   │
│  │Onboarding│  │ 35 tools │  │session   │  │              │   │
│  │Need Coord│  │organized │  │profile   │  │ Validates    │   │
│  │Memory    │  │in 10     │  │memory    │  │ every input  │   │
│  │Summarizer│  │categories│  │identity  │  │ before it    │   │
│  │Returning │  │          │  │need      │  │ reaches      │   │
│  │Volunteer │  │          │  │coord     │  │ service code │   │
│  └──────────┘  └──────────┘  │school    │  └──────────────┘   │
│                               │telemetry │                      │
│                               └──────────┘                      │
└─────────────────────────────────────────────────────────────────┘
```



#### What the LLM Actually "Sees" as Context

```
LLM CONTEXT WINDOW (in-memory, per request)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  System Prompt (from @mcp.prompt)                        │
│  ─────────────────────────────────                       │
│  "You are the Serve Onboarding Assistant.                │
│   Ask one question at a time. Confirm before saving..."  │
│                          ↑                               │
│                 Loaded from MCP Prompts                  │
│                                                          │
│  + Memory Summary (loaded via get_memory_summary)        │
│  ─────────────────────────────────────────────────       │
│  "Priya, teaches maths, available weekends..."           │
│                          ↑                               │
│                 Agent explicitly calls this tool         │
│                                                          │
│  + Current Profile State (from get_missing_fields)       │
│  ──────────────────────────────────────────────          │
│  "Still missing: time_preferred, availability"           │
│                                                          │
│  + Last N messages (from get_conversation)               │
│  ─────────────────────────────────                       │
│  [user]: "I can do weekends"                             │
│  [assistant]: "Which time — morning or evening?"         │
│  [user]: "Morning"                                       │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

The agent must load these tools, MCP doesn't automatically inject them. The agent calls `resume_session` which returns session state, then `get_memory_summary`, then `get_conversation`. After that the LLM has full context.

#### Two-Layer Context Strategy&#x20;

```
SHORT-TERM CONTEXT              LONG-TERM CONTEXT
(within a session)              (across sessions)

conversation_messages           memory_summaries
┌──────────────────┐            ┌──────────────────────────┐
│ Full chat log    │            │ Compressed facts          │
│ stored in DB     │            │ "Priya, maths, Blr..."    │
│                  │            │                          │
│ Agent loads last │            │ Agent loads this at the  │
│ 20-50 messages   │            │ START of every new       │
│ into LLM window  │            │ session for this user    │
└──────────────────┘            └──────────────────────────┘

         +

volunteer_profiles / need_drafts
┌──────────────────────────────────────┐
│ Structured state                     │
│ (not free text, queryable)           │
│                                      │
│ Agent calls get_missing_fields()     │
│ to know exactly what's still needed  │
│ without re-reading full history      │
└──────────────────────────────────────┘
```
