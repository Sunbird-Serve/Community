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



* Core 8-step flow: resume/create session → save user message → route to agent → invoke agent → validate state transition → save response → handle handoffs → return response
