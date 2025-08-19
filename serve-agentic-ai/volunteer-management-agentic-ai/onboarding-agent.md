# Onboarding Agent

### Objectives

* **Objectives/Goals**: (1) Welcome & set expectations, (2) Collect essentials for screening & matching, (3) Verify contacts/timezone, (4) Schedule _Volunteer Selection Discussion_ screening call, (5) Persist profile with audit trail.

### Responsibilities & Interfaces

* **Primary responsibilities**
  1. Conversational intake (slot‑filling → profile schema)
  2. Contact verification (OTP/email) & timezone capture
  3. Pre screening eligibility check (rules)
  4. Screening meeting coordination (slots, invite, reminders)
  5. Persistence & event emission
* **Inputs**: `volunteer.registered.v1 { userId }`
* **Outputs (events)**: `onboarding.started.v1`, `userprofile.updated.v1`, `screening.meeting.scheduled.v1`, `onboarding.completed.v1`
* **Downstream dependency**: Screening Agent consumes `onboarding.completed.v1`

### Architecture with MCP

#### 1) Agentic Layer (Orchestrator)

* **Components**: Event Consumer, **Orchestrator** (workflows/state), Agent Policies (Onboarding/Screening/Fulfillment), Rule Engine, Retry/Idempotency Manager.
* **Owns**: Business logic, state transitions, event emission, human-in-the-loop steps, guardrails, SLAs.
* **Input**: Domain events (e.g., `volunteer.registered.v1`).
* **Output**: Domain events (e.g., `onboarding.completed.v1`), tool intents (calls to MCP Client).
* **Does NOT**: Talk directly to external APIs or databases.

#### 2) MCP Layer (Protocol & Tool Invocation)

* **MCP Client** :
  * Translates tool intents into protocol compliant requests, handles schemas, auth, retries, timeouts.
  * Enforces input/output validation and contracts.
* **MCP Server** :
  * Exposes curated tools: `userprofile.get/update`, `comms.send`, `calendar.findSlots/schedule`, `meet.create`, `otp.send/verify`, `timezone.detect`, etc.
  * Manages connectors, secrets, rate limits; isolates side effects.
* **Contracts**: JSON Schemas for each tool input/output, SDL/manifest for discovery.

#### 3) Stores/Services

* **SERVE Volunteering Service, Comms (Email/WA/SMS), Calendar, Meeting (Meet), OTP, Timezone**
* **Owns**: Persistence, external effects, APIs.
* **Does NOT**: Contain business workflow decisions.

####

<figure><img src="../../.gitbook/assets/Onboarding Agent _ Mermaid Chart-2025-08-18-055409.png" alt=""><figcaption></figcaption></figure>

#### A) Trigger & Context (Agentic Layer)

1. **Event Consumer** receives `volunteer.registered.v1 { volunteerId }`.
2. It forwards the event to the **Onboarding Orchestrator** and creates a **run context** (idempotency key = `volunteerId`, correlation id, timestamps).

#### B) Orchestrate → Policy (Agentic Layer)

3. The Orchestrator starts the **Onboarding Agent Policy** (task decomposition logic) with the run context.
4. Policy asks Orchestrator to run an **LLM slot-filling prompt** (simple chat) to gather subjects, grades, languages, availability/time-zone hints, device/bandwidth, experience, consent.
   * Orchestrator validates outputs against enums/regex and returns **validated fields** to Policy.

#### C) First communications & profile load (MCP layer + services)

5. Policy raises a **tool intent: `comms.send("welcome", to)`** → **MCP Client** → **MCP Server** → **Comms** (Email/WA/SMS). Welcome message goes out with “what happens next”.
6. Policy raises **`profile.get(volunteerId)`** → MCP → **User Profile API** to fetch the draft profile.

#### D) Contact verification (MCP + services)

7. Policy requests **`otp.send(channel,to)`** → MCP → **Firebase OTP**; receives `otpId`.
8. Policy requests **`otp.verify(otpId, code)`** when the volunteer replies; if verification fails after N attempts, Orchestrator records failure and moves to guidance.

#### E) Normalize & persist profile (MCP + services)

9. Policy requests **`timezone.detect(freeText/phoneCountry)`** → MCP → **Timezone Resolver** to normalize availability windows.
10. Policy composes a **complete profile** (existing + validated fields + timezone + verification status) and calls **`userprofile.upsert(profileComplete)`** → MCP → **User Profile API** (idempotent on `volunteerId`).
11. Orchestrator emits **`userprofile.updated.v1`** for audit/telemetry.

#### F) Schedule the screening call (MCP + services)

13. Policy requests **`calendar.findSlots(volunteerId)`** → MCP → **Calendar** (offer 2–3 candidate slots that intersect volunteer availability + interviewer windows).
14. Policy requests **`meet.create("Volunteer Selection Discussion")`** → MCP → **GMeet** to obtain a `meetingLink`.
15. Policy requests **`calendar.schedule(slot, attendee, meetingLink)`** → MCP → **Calendar** to create the invite (title: _Volunteer Selection Discussion_, agenda, interviewer brief).
16. Orchestrator emits **`screening.meeting.scheduled.v1 { volunteerId, scheduledAt, meetingLink }`**.

#### G) Confirmations & reminders (MCP + services)

17. Policy requests **`comms.send("screening_confirm+ICS", to)`** → MCP → **Comms** (sends calendar ICS, prep checklist, auto-reminders T-24h/T-2h/T-10m configured by template).

#### H) Exit (Agentic Layer)

18. Orchestrator marks status `onboarding_complete` and emits **`onboarding.completed.v1`**.
19. **Done.** The **Screening Agent** will later consume `onboarding.completed.v1` / `screening.meeting.scheduled.v1`.

***

### Capabilities

* **Agentic Layer :** event handling, LLM slot-filling & validation, rules/eligibility, idempotency/retries, and **all domain events** (`userprofile.updated.v1`, `onboarding.blocked.v1`, `screening.meeting.scheduled.v1`, `onboarding.completed.v1`).
* **MCP Client/Server (protocol & effects):** executes **tool intents** from Policy: `comms.send`, `userprofile.get/upsert`, `otp.send/verify`, `timezone.detect`, `calendar.findSlots/schedule`, `meet.create`.
* **Services:** Volunteering API, Comms, Calendar, GMeet, Firebase OTP, Timezone Resolver.

***

### Failure/edge handling

**will be added soon**
