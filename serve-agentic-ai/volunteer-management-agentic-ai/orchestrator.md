# Orchestrator

### Objectives

**Objectives/Goals:**

1. Govern the full volunteer lifecycle (registered → onboarded → screened → assigned).
2. Route events to the correct Agent Policy (Onboarding, Screening, Fulfillment).
3. Maintain volunteer journey state with retries, idempotency, and escalation paths.
4. Enforce sequencing rules and policy guardrails.
5. Emit telemetry and cross-domain events (`need.assigned`, `volunteer.state.updated`).
6. Provide continuity of context & memory across all agents.

***

### Responsibilities & Interfaces

**Primary responsibilities:**

* Event ingestion & dispatch to agents.
* State machine for volunteer journey.
* Guardrails: retries, SLAs, error handling, human escalation.
* Apply policy rules before transitions.
* Emit audit and telemetry events for observability.

**Inputs:**

* `volunteer.registered.v1` (from Volunteering Service)
* `onboarding.completed.v1` (from Onboarding Agent)
* `screening.completed.v1` (from Screening Agent)
* `fulfillment.completed.v1` (from Fulfillment Agent)

**Outputs (events):**

* `onboarding.started.v1`, `screening.started.v1`, `fulfillment.started.v1`
* `volunteer.state.updated.v1`, `need.assigned.v1`
* Escalations: `onboarding.blocked.v1`, `screening.failed.v1`, `fulfillment.escalated.v1`

**Downstream dependency:**

* Agents depend on Orchestrator for state context & domain events.
* Need-Coordinator Orchestrator consumes `need.assigned.v1`.

***

### Architecture with MCP

**1) Agentic Layer (Orchestrator Core)**

* Components: Event Consumer, State Machine, Agent Router, Rule Engine, Retry/Idempotency Manager.
* Owns: Routing, transitions, escalation, sequencing, telemetry.
* Input: Domain events.
* Output: Domain events, Agent triggers.
* Does NOT: Call external APIs directly.

**2) MCP Layer (Protocol & Tool Invocation)**

* Orchestrator itself doesn’t invoke tools.
* Instead, delegates to Agents, which raise tool intents.
* MCP Client/Server manage schemas, retries, and API connectors.

**3) Context & Memory**

* Context Store: volunteer state, correlation ids, timestamps.
* Memory Map:
  * Short-term = run context (e.g., retry attempts, OTP tries).
  * Long-term = volunteer journey (registered → assigned).
* Orchestrator ensures continuity across agents.

***

### Detailed Walk-through (Orchestrator View)

| Phase & Action                                            | Assistant Agent  | MCP Tool Calls                                | Key Decisions / Errors                                                                      |
| --------------------------------------------------------- | ---------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1. Registration event (`volunteer.registered.v1`) arrives | —                | —                                             | Orchestrator sets volunteer state = NEW                                                     |
| 2. Trigger Onboarding                                     | OnboardingAgent  | comms.send (welcome)                          | Retry policy (2 × 24h), escalation after 3rd failure                                        |
| 3. Transition → Screening                                 | ScreeningAgent   | calendar.schedule, meet.create                | No-show retried once; second miss → escalate                                                |
| 4. Screening outcome                                      | ScreeningAgent   | LLM scoring, profile update                   | Decision: recommend / hold / reject                                                         |
| 5. Transition → Fulfillment                               | FulfillmentAgent | needDiscovery, fulfillment.assign             | If no fit → backlog report                                                                  |
| 6. Assignment complete                                    | FulfillmentAgent | fulfillment.assign, volunteering.updateStatus | Orchestrator marks state = ASSIGNED, emit `need.assigned.v1`                                |
| 7. Telemetry                                              | —                | —                                             | Emit telemetry at every state (`welcome_sent`, `screening.scheduled`, `assignment_success`) |

***

### Capabilities

**Agentic Layer:**

* Event handling, routing, sequencing, retries/idempotency, escalation, telemetry.
* Governs state transitions across all 3 agents.

**MCP Client/Server:**

* Orchestrator does not directly call tools, but depends on MCP contracts.
* Guarantees schema validation, retries, error handling for agents’ tool intents.

**Services:**

* Consumed indirectly via agents (Volunteering API, Comms, Calendar, GMeet, Firebase OTP, NeedService, FulfillService).
