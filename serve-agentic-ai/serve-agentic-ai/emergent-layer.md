# Emergent Layer

```
+----------------------------------------------------------------------------------+
|                            Product / Ops / VM Inputs                             |
|----------------------------------------------------------------------------------|
| - define new agent idea                                                          |
| - define MVP tasks and workflow                                                  |
| - define prompts, handoffs, business rules                                       |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                                     Emergent                                     |
|----------------------------------------------------------------------------------|
| Rapid agent-building / prototyping layer                                         |
| - design workflows                                                               |
| - define prompts and decision logic                                              |
| - test handoffs between agents                                                   |
| - simulate agent behavior                                                        |
| - validate integration flow before coding                                        |
+--------------------------+---------------------------+---------------------------+
                           |                           |
                           | Prototype / validate      | Generate / refine logic
                           |                           |
                           v                           v
+------------------------------------------------+   +----------------------------------+
|         Prototype Agent Workflows              |   |      Current SERVE Codebase      |
|------------------------------------------------|   |----------------------------------|
| - Engagement Agent prototype                   |   | - existing orchestrator          |
| - Delivery Support Agent prototype                   |   | - onboarding agent               |
| - Need Agent prototype                         |   | - selection agent                |
| - Fulfillment Agent prototype                  |   | - new prod agents when ported    |
+----------------------+-------------------------+   +------------------+---------------+
                       |                                                |
                       | Calls real tools / APIs                        |
                       +----------------------+-------------------------+
                                              |
                                              v
+----------------------------------------------------------------------------------+
|                         Shared SERVE Integration / Tool Layer                     |
|----------------------------------------------------------------------------------|
| - volunteer profile / status APIs                                                |
| - need / fulfilment APIs                                                         |
| - nomination / assignment APIs                                                   |
| - WhatsApp send / receive endpoints                                              |
| - telemetry                                                                      |
| - MCP tools                                                                      |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                              Current SERVE AI                                    |
|----------------------------------------------------------------------------------|
| WhatsApp Gateway                                                                 |
|        ↓                                                                         |
| Orchestrator                                                                     |
|        ↓                                                                         |
| Agents                                                                           |
| - Onboarding Agent                                                               |
| - Selection Agent                                                                |
| - Engagement Agent                                                               |
| - Fulfilment Agent                                                               |
| - Need Agent                                                                     |
|        ↓                                                                         |
| Session / State                                                                  |
|        ↓                                                                         |
| Telemetry / Event Store / DB                                                     |
+-----------------------------------+----------------------------------------------+
                                    |
                                    v
+----------------------------------------------------------------------------------+
|                               Deployment Layer                                   |
|----------------------------------------------------------------------------------|
| - Emergent as sandbox / experimentation layer                                    |
| - SERVE codebase as production deployment path                                   |
| - validated logic can be ported from prototype to repo                           |
+----------------------------------------------------------------------------------+
```
