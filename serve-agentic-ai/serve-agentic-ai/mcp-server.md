# MCP Server

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
