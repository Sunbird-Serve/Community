# Onboarding Agent

### Objectives

* **Objectives**: (1) Welcome & set expectations, (2) Collect essentials for screening & matching, (3) Verify contacts/timezone, (4) Schedule _Volunteer Selection Discussion_ screening call, (5) Persist profile with audit trail.

### Responsibilities & Interfaces

* **Primary responsibilities**
  1. Conversational intake (slot‑filling → profile schema)
  2. Contact verification (OTP/email) & timezone capture
  3. Pre‑screening eligibility check (rules)
  4. Screening meeting coordination (slots, invite, reminders)
  5. Persistence & event emission
* **Inputs**: `volunteer.registered.v1 { userId }`
* **Outputs (events)**: `onboarding.started.v1`, `profile.updated.v1`, `screening.meeting.scheduled.v1`, `onboarding.completed.v1`
* **Downstream dependency**: Screening Agent consumes `onboarding.completed.v1`

### Architecture with MCP

#### 1) Agentic Layer (Orchestrator)

* **Components**: Event Consumer, **Orchestrator** (workflows/state), Agent Policies (Onboarding/Screening/Fulfillment), Rule Engine, Retry/Idempotency Manager.
* **Owns**: Business logic, state transitions, event emission, human-in-the-loop steps, guardrails, SLAs.
* **Input**: Domain events (e.g., `volunteer.registered.v1`).
* **Output**: Domain events (e.g., `onboarding.completed.v1`), tool intents (calls to MCP Client).
* **Does NOT**: Talk directly to external APIs or databases.

#### 2) MCP Layer (Protocol & Tool Invocation)

* **MCP Client** (inside Agentic Layer process):
  * Translates tool intents into protocol-compliant requests, handles schemas, auth, retries, timeouts.
  * Enforces input/output validation and contracts.
* **MCP Server** (tool host):
  * Exposes curated tools: `userprofile.get/update`, `comms.send`, `calendar.findSlots/schedule`, `meet.create`, `otp.send/verify`, `timezone.detect`, etc.
  * Manages connectors, secrets, rate limits; isolates side effects.
* **Contracts**: JSON Schemas for each tool input/output, SDL/manifest for discovery.

#### 3) Stores/Services (Effectors)

* **SERVE Volunteering Service, Comms (Email/WA/SMS), Calendar, Meeting (Meet/Jitsi), OTP, Timezone**
* **Owns**: Persistence, external effects, APIs.
* **Does NOT**: Contain business workflow decisions.

####

<figure><img src="../../.gitbook/assets/Onboarding Agent _ Mermaid Chart-2025-08-18-055409.png" alt=""><figcaption></figcaption></figure>
