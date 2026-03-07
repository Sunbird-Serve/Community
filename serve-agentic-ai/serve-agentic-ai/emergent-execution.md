# Emergent - Execution

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

**Onboarding Agent**

Goal - Guide a volunteer through initial onboarding in a conversational way, collect required baseline details, build trust, and complete onboarding so the volunteer can move to the next stage.

User details

* Volunteer
* First-time user
* May be curious, hesitant, busy, or only partially committed
* May respond in short, informal, typo-filled language
* May pause and return later

Guardrails - Do not mark onboarding complete unless mandatory fields are captured, Do not invent or assume volunteer details, Do not repeat already confirmed questions, Do not overwhelm with too many questions in one turn, Do not continue endlessly if user clearly wants to pause, Do not promise assignment or selection at this stage, Keep responses concise and warm

About Eligibility? Any highlevel workflow? what data to be collected? MCP Tools required, telemetry events?

Handoff Logic - Handoff to **Selection Agent** when onboarding is complete, Pause if user says later / busy / not now, Handoff to human if policy confusion, complaint, or unsupported scenario arises

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
