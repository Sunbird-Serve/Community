# Screening Agent

#### Objectives

* Evaluate and validate volunteers after onboarding to confirm eligibility and readiness for matching.
* Facilitate live or asynchronous screening discussions based on set criteria.
* Update volunteer profile with screening status and emit domain events for downstream systems.

#### Responsibilities & Interfaces

* **Primary responsibilities**
  1. Initiate screening conversation (slot-filling or Q\&A)
  2. Coordinate and schedule screening sessions (calls or questionnaires)
  3. Conduct pre-screening eligibility checks (via rules or simple scoring)
  4. Record outcomes and update profile status (pass/fail/pending)
  5. Emit relevant domain events (screening.started, passed, failed, etc.)
* **Inputs**: `onboarding.completed.v1 { volunteerId }`
* **Outputs (events)**:
  * `screening.started.v1`
  * `screening.meeting.scheduled.v1` (if live session)
  * `screening.completed.v1`
  * Depending on outcome: `screening.passed.v1`, `screening.failed.v1`, or `screening.retry.v1`
* **Downstream dependency**: Fulfillment Agent consumes `screening.passed.v1`

#### Architecture with MCP

**1) Agentic Layer (Orchestrator)**

* **Components**: Event Consumer, Orchestrator (workflows/state), Agent Policy (Screening), Rule Engine, Retry/Idempotency Manager.
* **Owns**: Business logic, state transitions, LLM calls (if used), event emission, human-in-the-loop steps and SLAs.
* **Inputs**: Domain event `onboarding.completed.v1`
* **Outputs**: Domain events such as `screening.passed.v1`, and tool intents (e.g., comms requests, calendar invites)

**2) MCP Layer (Protocol & Tool Invocation)**

* **MCP Client**: Translates tool intents into protocol-compliant requests, ensures validation, handles retries/timeouts.
* **MCP Server**: Hosts tools like `comms.send`, `calendar.findSlots/schedule`, `meet.create`, `form.send/collect`, `userprofile.get/upsert`, etc.

**3) Stores/Services**

* **Services involved**: Comms (Email/WA/SMS), Calendar, Meeting (e.g., GMeet), Questionnaire/Form service, User Profile API, plus any scoring/rule engines.
* **Responsibilities**: Persistence, external communication, scheduling, scoring, profile updates.

#### Agentic Flow

<figure><img src="../../.gitbook/assets/Architecture - Agentic AI _ Mermaid Chart-2025-08-18-085400.png" alt=""><figcaption></figcaption></figure>

A) **Trigger & Context (Agentic Layer)**

1. Event Consumer receives `onboarding.completed.v1 { volunteerId }`
2. Forwards to Screening Orchestrator, creates run context (idempotency key, correlation ID, timestamps)

B) **Orchestrate → Policy (Agentic Layer)**

1. Orchestrator starts the Screening Agent Policy with the run context
2. Policy may initiate screening via:
   * LLM-based questionnaire or guided intake, **or**
   * Switch to live session scheduling depending on volunteer/organization preference

C) **Screening Initiation (MCP + Services)**

1. Policy sends tool intent: `comms.send("screening.started", to)` → MCP → Comms service
2. Optionally:
   * `form.send("screening.questionnaire")`
   * **or** `calendar.findSlots(volunteerId)` → MCP → Calendar
   * And `meet.create("Volunteer Screening Session")` → MCP → Meeting service
   * Then `calendar.schedule(slot, attendee, meetingLink)` → MCP → Calendar
3. Emit `screening.meeting.scheduled.v1 { volunteerId, scheduledAt, meetingLink }` if a live session is involved

D) **Screening Execution (MCP + Services)**

* If using questionnaire: wait for submission, collect responses via `form.collect`
* If live session: wait for meeting completion, log attendance

E) **Evaluate & Update (Agentic + MCP Layers)**

1. Policy evaluates responses or real-time discussion outputs using rules or document AI
2. Sets outcome status: **Pass**, **Fail**, **Retry**
3. Updates profile via `userprofile.upsert({ volunteerId, screeningStatus })` through MCP
4. Emit appropriate event: `screening.passed.v1`, `screening.failed.v1`, or `screening.retry.v1`

F) **Exit (Agentic Layer)**

* Mark status as `screening_complete` and finalize run

#### Capabilities

* **Agentic Layer**: event handling, task orchestration, rule-based decisions, idempotency/retries, emitting screening events and profile updates.
* **MCP Client/Server**: executes tool intents (`comms.send`, `form.send/collect`, `calendar.findSlots/schedule`, `meet.create`, `userprofile.get/upsert`).
* **Services**: Comms service, Form service, Calendar, Meeting, User Profile API, Scoring/Rule Engine.

#### Failure / Edge Handling

will be added soon
