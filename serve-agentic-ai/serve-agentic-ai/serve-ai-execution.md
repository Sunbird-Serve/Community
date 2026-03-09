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

**Orchestrator**&#x20;

**Goal:** Coordinate the lifecycle of interactions across the Serve-AI system by identifying the correct workflow, selecting the right active agent, preserving context, enforcing valid stage transitions, managing handoffs, and ensuring each interaction progresses toward the correct operational outcome.

**Persona:** Multi-persona(new volunteer, onboarded volunteer, recommended / inactive volunteer, need coordinator, system-triggered events, scheduled reminders / nudges), channel-agnostic(channel inputs from web or WhatsApp).  Coordination focused, not conversational

**Data:** session, workflow, stage, active agent, status, linked entities(volunteer\_id, coordinator\_id, need\_id, assignment\_id), context summary

**Guardrails:** no business reasoning, no invalid transitions, no direct conversational logic - This will evolve

**Handoff Logic:** validate and execute agent/stage transitions safely -&#x20;

* agent-to-agent handoff validation
* session pause/resume transitions
* escalation to human/ops routing
* system-triggered workflow activation

**MCP Tools:** session, workflow validation, context retrieval, escalation, telemetry

**Memory & Telemetry:** memory, routing/state/handoff/session events

**Onboarding Agent**

Goal - Discover the intent, orient them with the available nature of needs, have them sign up for the purpose behind the needs. The purpose of the needs here is enabling equitable access to quality education.&#x20;

discover their capabilities(around skills, educational qualification, work and volunteer experiences and language proficiency) to volunteer for a need and their mandatory perquisites which are legal adult and willing to give time as a volunteer without pay.&#x20;

User details - Men and Women who are working professionals, students, senior citizens or home makers. belong to age group of 18 to 75

Guardrails - Do not mark onboarding complete unless mandatory fields are captured, Do not invent or assume volunteer details, Do not repeat already confirmed questions, Do not overwhelm with too many questions in one turn, Do not continue endlessly if user clearly wants to pause, Do not promise assignment or selection at this stage, Keep responses concise and warm

MCP Tools required - Firebase for auth, serve\_user&#x20;

**Selection Agent**

Goal - Assess whether an onboarded volunteer is suitable and ready for the next step through a conversational evaluation, and produce a recommendation such as recommended, not matched, or human review.

User - Volunteer who completed onboarding, May be enthusiastic, uncertain, or overconfident, May have varying communication clarity

Data to be collected ?? Rubrics? like teaching readiness, commitment, motivational depth etc.. data like subject comfort, language, time commitment etc?&#x20;

Guardrails - Do not show scoring or internal rubric logic directly, Do not reject harshly or in discouraging language, Do not bypass required evaluation dimensions, Escalate when responses are too ambiguous or contradictory

Handoff Logic - Handoff to Fulfillment Agent  if recommended.&#x20;

MCP Tools, Telemetry events?&#x20;

**Fulfillment Agent**

Goal - Assist all the recommended volunteers to nominate a need.. Match the needs based on their preference. Rule engine? This can be a goal?&#x20;

User - Volunteer who are recommended. This agent would assist the need coordinator also?&#x20;

**Engagement Agent** - [Link](engagement-agent.md)

**Need Agent** - [Link](need-agent.md)

**Delivery Assistant Agent** - [Link ](delivery-support-agent.md)
