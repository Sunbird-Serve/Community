# Orchestrator

**Goal:** Coordinate the lifecycle of interactions across the Serve-AI system by identifying the correct workflow, selecting the right active agent, preserving context, enforcing valid stage transitions, managing handoffs, and ensuring each interaction progresses toward the correct operational outcome.

```
Channels [Web UI, Whatsapp, Mobile App]
   ↓
Channel Adapter [Normalize]
   ↓
Orchestrator Discovery
[Resolve Persona + Session State + Intent]
   ↓
Determine which agent should own this interaction
   ↓
Route to Agent
```

```
+----------------------------------------------------------------------------------+
|                                   CHANNELS                                       |
|----------------------------------------------------------------------------------|
|  Web UI / WhatsApp / Scheduler / Mobile App                                      |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                               CHANNEL ADAPTER                                    |
|----------------------------------------------------------------------------------|
|  Normalize incoming input into common format                                     |
|  - actor id                                                                       |
|  - channel                                                                        |
|  - trigger type                                                                   |
|  - payload / message                                                              |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                           ORCHESTRATOR DISCOVERY                                 |
|----------------------------------------------------------------------------------|
|  Resolve Persona  ↔  Resolve Session State  ↔  Resolve Intent                    |
|                                                                                  |
|  Persona: Volunteer / Coordinator / Ops / System                                 |
|  Session State: Active / Paused / No session                                     |
|  Intent: What does the actor want now?                                           |
|                                                                                  |
|  Output: Which agent owns this persona + session state + intent                  |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                                AGENT ROUTING                                     |
|----------------------------------------------------------------------------------|
|  Route to the appropriate agent                                                  |
|  - Primary agent (Onboarding, Selection, Fulfillment, Need Agent, Delivery 
Assistant) |
|  - Cross-cutting support agent (Engagement Agent, Helpline Agent)                |
+----------------------------------------------------------------------------------+
```

Volunteer Flow

```
New Volunteer → Onboarding → Selection → Fulfillment → Delivery
                     |            |            |
                     |            |            |
                     +------------+------------+
                                  |
                              Engagement
                                  ↑
                                  |
     Recommended but not utilised / Inactive Volunteer
           |                          |
           |                          |
           |                          +---- Re-entry to Onboarding / Selection / Fulfillment
           |
           +---- Re-entry to Fulfillment
           
     Returning Volunteer
        ↓
Resolve current stage / intent
        ↓
Re-enter appropriate node
(Onboarding / Selection / Fulfillment / Delivery / Engagement)
```

**Entry mapping:**

| Volunteer Type               | Entry Agent                                       |
| ---------------------------- | ------------------------------------------------- |
| New Volunteer                | Onboarding                                        |
| Returning Volunteer          | Resolve stage → appropriate node                  |
| Recommended but not utilised | Engagement → Fulfillment                          |
| Inactive Volunteer           | Engagement → Onboarding / Selection / Fulfillment |

**Need Coordinator Flow**

```
nCoordinator → Need → Fulfillment → Delivery
                        |            |
                        |            |
                        +------------+
                             |
                         Delivery
                             ↑
                             |
            nCoordinator / Session Updates
                             |
                             +---- Re-entry to Need / Fulfillment
```

**Persona:** Multi-persona(new volunteer, onboarded volunteer, recommended / inactive volunteer, need coordinator, system-triggered events, scheduled reminders / nudges), channel-agnostic(channel inputs from web or WhatsApp).  Coordination focused, not conversational

**Data:** session, workflow(multi workflow), stage, active agent, status, linked entities(volunteer\_id, coordinator\_id, need\_id, assignment\_id), context summary

**Guardrails:** no business reasoning, no invalid transitions, no direct conversational logic - This will evolve

**Handoff Logic:** validate and execute agent/stage transitions safely -&#x20;

* agent-to-agent transitions
* resume/re-entry transitions
* temporary support invocations
* escalation to human/ops
* system-triggered workflow activations

**MCP Tools:** session, workflow validation, context retrieval, escalation, telemetry, persona selection

**Memory & Telemetry:** memory, routing/state/handoff/session events



Core 8-step flow: resume/create session → save user message → route to agent → invoke agent → validate state transition → save response → handle handoffs → return response

#### The Big Picture: What Files Do What

```
serve-orchestrator/
│
├── main.py                          ← FastAPI app, startup, MCP proxy
├── app/api/orchestrator_routes.py   ← HTTP endpoints (/interact, /session)
│
├── app/channel/
│   ├── adapters.py                  ← Normalize raw input → common format
│   └── registry.py                  ← Maps channel → right adapter
│
├── app/service/
│   ├── orchestration.py             ← THE CORE BRAIN (8-step flow)
│   ├── intent_resolver.py           ← "What does the user want?"
|   |-- persona_resolver.py          ← "Who is the user?"
│   ├── agent_router.py              ← "Which agent handles this?"
│   └── workflow_validator.py        ← "Is this state change allowed?"
│
├── app/clients/
│   ├── domain_client.py             ← Talks to MCP (sessions, messages)
│   └── agent_client.py              ← (Agent HTTP calls)
│
└── app/schemas/
    └── orchestrator_schemas.py      ← All data models (request/response shapes)
```

***

#### Layer-by-Layer Flow

```
USER SENDS A MESSAGE
        │
        ▼
┌───────────────────────────────────────────────────┐
│              HTTP API LAYER                        │
│   POST /api/orchestrator/interact                  │
│   (orchestrator_routes.py)                         │
│                                                   │
│   Receives: InteractionRequest                    │
│   { session_id, message, channel, channel_metadata│
│     persona }                                     │
└──────────────────────┬────────────────────────────┘
                       │
                       ▼
┌───────────────────────────────────────────────────┐
│           CHANNEL ADAPTER LAYER                   │
│   (channel/adapters.py + registry.py)             │
│                                                   │
│   Web UI   → WebUIAdapter    (actor = email_id)    │
│   WhatsApp → WhatsAppAdapter (actor = phone num)  │
│   Scheduler→ SchedulerAdapter(actor = job_id)     │
│   Mobile   → MobileAdapter   (actor = phone num) │
│   API      → APIAdapter      (actor = client_id) │
│                                                   │
│   Output: NormalizedEvent                         │
│   { actor_id, channel, trigger_type,              │
│     payload, session_id, persona? }               │
└──────────────────────┬────────────────────────────┘
                       │
                       ▼
┌───────────────────────────────────────────────────┐
│         ORCHESTRATION CORE  (orchestration.py)    │
│                                                   │
│  GUARD: Idempotency Check                         │
│    → Duplicate WhatsApp/webhook delivery? → drop  │
│                                                   │
│  STEP 1: Persona Resolution  ─────────────────────┼──→ persona_resolver.py
│    (new sessions only — resumed sessions          │    (async, uses MCP lookup)
│     restore persona from storage)                 │
│    → channel sent explicit persona?  → use it     │
│    → SCHEDULED / SYSTEM trigger?     → SYSTEM     │
│    → actor found in MCP registry?                 │
│         coordinator record           → NEED_COORDINATOR
│         volunteer, inactive >90d     → INACTIVE_VOLUNTEER
│         volunteer, active            → RETURNING_VOLUNTEER
│    → no record found / MCP down      → NEW_VOLUNTEER
│    → stamps resolved persona onto NormalizedEvent │
│                                                   │
│  STEP 2: Session Resolution                       │
│    → Has session_id? → Resume (restore persona    │
│                         from storage)             │
│    → No session_id?  → Create new session         │
│      (persona → workflow → initial agent)         │
│      NEW_VOLUNTEER      → onboarding workflow     │
│      RETURNING_VOLUNTEER→ returning_volunteer wf  │
│      NEED_COORDINATOR   → need_coordination wf    │
│    (via MCP server through domain_client)         │
│                                                   │
│  STEP 3: Intent Resolution  ──────────────────────┼──→ intent_resolver.py
│    → "What does the user want right now?"         │    
│    START_WORKFLOW / CONTINUE / RESUME /            │
│    PAUSE / ESCALATE / RESTART / SEEK_HELP         │
│                                                   │
│  STEP 4: Terminal Intent Short-circuit            │
│    PAUSE    → save progress, say goodbye          │
│    ESCALATE → flag for human, freeze session      │
│    RESTART  → create fresh session, start over    │
│                                                   │
│  STEP 5: Save User Message (to MCP)               │
│                                                   │
│  STEP 6: Agent Routing ───────────────────────────┼──→ agent_router.py
│    → Which agent handles this persona+stage?      │
│    SEEK_HELP  → current agent, low confidence     │
│    returning_volunteer → engagement (or fallback) │
│    otherwise  → agent that owns current stage     │
│                                                   │
│  STEP 7: Invoke Agent (HTTP POST /api/turn)       │
│    → Send AgentTurnRequest (+ intent_hint)        │
│    → Receive AgentTurnResponse                    │
│                                                   │
│  STEP 8: Validate State Transition ───────────────┼──→ workflow_validator.py
│    → Is stateA → stateB allowed in this workflow? │
│    → If yes: persist new state via MCP            │
│                                                   │
│  STEP 9: Save Agent Reply (to MCP)                │
│                                                   │
│  STEP 10: Handle Handoff (if any)                 │
│    → Agent signals "pass to next agent"           │
│    → Persist new active_agent in session          │
│                                                   │
│  STEP 11: Build & Return InteractionResponse      │
│    debug_info includes:                           │
│      persona { value, confidence, source }        │
│      intent  { type, confidence, signal }         │
│      routing { target_agent, confidence, reason } │
│      timing_ms, telemetry_events                  │
└───────────────────────────────────────────────────┘
```

#### Persona Resolver

```
1. Explicit persona in request       → trust it (confidence 1.0)
2. SCHEDULED / SYSTEM_TRIGGER        → SYSTEM (confidence 1.0)
3. MCP actor lookup by actor_id      →
     coordinator record found        → NEED_COORDINATOR  (0.95)
     volunteer, inactive > 90 days   → INACTIVE_VOLUNTEER (0.90)
     volunteer, active               → RETURNING_VOLUNTEER (0.95)
4. No record found / MCP unavailable → NEW_VOLUNTEER (0.80)
```

#### Intent Resolver

```
User message arrives
        │
        ├─ No session exists?        → START_WORKFLOW     (confidence 1.0)
        ├─ Scheduled/system trigger? → CONTINUE_WORKFLOW  (confidence 0.95)
        ├─ Session is PAUSED?        → RESUME_SESSION     (confidence 0.95)
        ├─ Says "talk to a human"?   → ESCALATE           (confidence 0.88)
        ├─ Says "start over"?        → RESTART            (confidence 0.88)
        ├─ Says "bye/pause/stop"?    → PAUSE_SESSION      (confidence 0.83)
        ├─ Says "help/confused"?     → SEEK_HELP          (confidence 0.80)
        ├─ Says "continue/I'm back"? → RESUME_SESSION     (confidence 0.75)
        └─ Anything else?            → CONTINUE_WORKFLOW  (confidence 0.90)
```

PAUSE, ESCALATE, RESTART are handled directly by the orchestrator, agents are never even called.

***

#### Agent Router&#x20;

```
Registered Agents:
┌─────────────────┬────────┬──────────────────────────────────────┐
│ Agent           │ Port   │ Status                               │
├─────────────────┼────────┼──────────────────────────────────────┤
│ onboarding      │  8002  │ HEALTHY (primary — new volunteers)   │
│ need            │  8005  │ HEALTHY (need coordinators)          │ 
└─────────────────┴────────┴──────────────────────────────────────┘

Routing Logic (in priority order):
1. SEEK_HELP intent  → keep current agent, confidence 0.75
2. returning_volunteer workflow → engagement agent
                               (fallback to onboarding if unavailable)
3. Current agent owns this stage → current agent, confidence 1.0
4. Stage-based lookup → find agent that owns this stage
5. Nobody matched → stay with current agent, confidence 0.5

Background: Every 30 seconds, probes /api/health on each agent
            and updates healthy/unhealthy status automatically.
```

#### Data Flow

```
Channel sends →  InteractionRequest
                 { session_id?, message, channel, channel_metadata, persona? }
                          │
                          ▼ (Channel Adapter)
                 NormalizedEvent
                 { actor_id, channel, trigger_type,
                   payload, session_id?, persona?, idempotency_key? }
                          │
                          ▼ (Orchestration Core)
                 AgentTurnRequest  (to agent)
                 { session_id, session_state, user_message,
                   conversation_history, intent_hint }
                          │
                          ▼ (from agent)
                 AgentTurnResponse
                 { assistant_message, active_agent, workflow, state,
                   confirmed_fields, missing_fields, handoff_event? }
                          │
                          ▼ (back to channel)
                 InteractionResponse
                 { session_id, assistant_message, active_agent, workflow,
                   state, status, is_complete, journey_progress, debug_info }
```

The orchestrator is the only piece that talks to the MCP server (for sessions and messages), to agents (via HTTP), and back to the channel. Agents and channels never talk to each other directly.
