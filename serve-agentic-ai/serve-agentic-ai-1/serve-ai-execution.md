# SERVE AI - Execution

```
+----------------------------------------------------------------------------------+
|                                   USER CHANNELS                                  |
|----------------------------------------------------------------------------------|
|  Web UI                                                                          |
|  - volunteer-facing chat                                                         |
|  - coordinator-facing chat / ops UI                                              |
|                                                                                  |
|  WhatsApp Channel                                                                |
|  - volunteer interactions                                                        |
|  - reminders / nudges / operational conversations                                |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                              CHANNEL ADAPTER LAYER                               |
|----------------------------------------------------------------------------------|
|  Web Adapter                                                                     |
|  WhatsApp Adapter                                                                |
|                                                                                  |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                               ORCHESTRATOR SERVICE                               |
|----------------------------------------------------------------------------------|
|  Single entry point for all incoming requests                                    |
|  - route request to correct agent                                                |
|  - manage handoffs between agents                                                |
|  - remain channel agnostic                                                       |  
|  - trigger telemetry events                                                      |
|                                                                                  |
|  Handoffs                                                                        |
|  - Onboarding → Selection                                                        |
|  - Selection → Fulfillment / Engagement                                          |
|  - Engagement -> Fulfillment                                                     |
|  - Need → Fulfillment                                                            |
|  - Delivery Assistant for reminders / operational support                        |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                                   MCP SERVER                                     |
|----------------------------------------------------------------------------------|
|  Shared tool and memory access layer for all agents                              |                                                                           |
|  Tool Details                                                                    |                                                                         |                                                                           |
|  Agents should use MCP tools, not directly write to DB                           |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                                  AGENT LAYER                                     |
|----------------------------------------------------------------------------------|
|  Onboarding Agent, Selection Agent, Fulfillment Agent, Engagement Agent, 
|  Delivery Assistant Agent, Need Agent              
|  1) Goal                                                                         |
|  2) User or Persona Details                                                      |
|  3) Data to be collected                                                         |
|  4) Gaurdrails                                                                   |
|  5) Handoff Logic                                                                |
|  6) MCP Tools required                                                           |
|  7) Memory context and telemetry events to emit                                  |
|  8) Worklow and architecture if any                                              |
|                                                                                  |
|                                                                                  |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                              SHARED DOMAIN / DATA LAYER                          |
|----------------------------------------------------------------------------------|
|  Core persistent stores                                                          |
|  - sessions                                                                      |
|  - session messages                                                              |
|  - volunteer profiles                                                            |
|  - coordinator / school context                                                  |
|  - needs                                                                         |
|  - nominations / assignments                                                     |
|  - agent state                                                                   |
|  - memory summaries                                                              |
|  - handoff history                                                               |
|  - telemetry / event store                                                       |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                         SHARED SERVE INTEGRATION - Through MCP Tools             |
|----------------------------------------------------------------------------------|
|  - volunteer profile / status APIs                                               |
|  - need APIs                                                                     |
|  - fulfilment / nomination APIs                                                  |
|  - WhatsApp send / receive APIs                                                  |
|  - telemetry                                                                     |
|  - Firebase, Gmail                                                               |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                                DEPLOYMENT LAYER                                  |
|----------------------------------------------------------------------------------|
|  Serve-AI modular services                                                       |
|  - ui-service                                                                    |
|  - adapter-service (web, whatsapp as clear separate components)                  |                                                             |
|  - orchestrator-service                                                          |
|  - mcp-server                                                                    |
|  - agent-service (All agents as clear separate components/modules)               |                                                                                                                   |
|  - postgres / persistent storage                                                 |
|                                                                                  |
|                                                                                  |
+----------------------------------------------------------------------------------+
```







