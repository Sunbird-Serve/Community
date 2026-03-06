# Fulfillment Agent

#### **Fulfillment Agent**

#### Objectives

* Match screened volunteers with active needs.
* Ensure matching respects eligibility, subject alignment, availability, and preferences.
* Trigger confirmation, scheduling, and communication flows for volunteer assignment.
* Emit events for tracking, telemetry, and downstream program operations.

#### Responsibilities & Interfaces

* **Primary responsibilities**
  1. Listen for `screening.passed.v1` event.
  2. Query available needs (via Need API/Registry).
  3. Match volunteer profile to needs using rules/AI scoring.
  4. Propose/auto-assign best-fit need.
  5. Send communication for confirmation.
  6. Update volunteer & need status in system.
  7. Emit fulfillment events (`fulfillment.assigned.v1`, etc.).
* **Inputs**
  * `screening.passed.v1 { volunteerId }`
* **Outputs (events)**
  * `fulfillment.started.v1`
  * `fulfillment.match.proposed.v1`
  * `fulfillment.assigned.v1`
  * `fulfillment.declined.v1`
  * `fulfillment.failed.v1`
* **Downstream dependency**
  * Comms services (to notify volunteer & school)
  * Scheduling/Meet tools (if first session auto-created)
  * Telemetry dashboards

#### Architecture with MCP

**1) Agentic Layer (Orchestrator)**

* **Owns**: matching logic, volunteer–need scoring, decision making, event emission.
* **Inputs**: `screening.passed.v1`
* **Outputs**: fulfillment events, tool intents (comms, scheduling).

**2) MCP Layer (Protocol & Tool Invocation)**

* **Executes** tool calls:
  * `profile.get(volunteerId)`
  * `need.findOpen()`
  * `need.assign(volunteerId, needId)`
  * `comms.send("assignment", to)`
  * `meet.create("class link")`

**3) Stores/Services**

* **Profile API** → Volunteer info, screening status, preferences.
* **Need API/Registry** → Open needs from schools/programs.
* **Comms Service** → Notifications (Email/WA/SMS).
* **Meeting Service** → Session setup.

#### Agentic Flow

<figure><img src="../../.gitbook/assets/Architecture - Agentic AI _ Mermaid Chart-2025-08-18-094052.png" alt=""><figcaption></figcaption></figure>

A) **Trigger & Context**

* Event Consumer receives `screening.passed.v1 { volunteerId }`.
* Fulfillment Orchestrator starts with run context (idempotency key = volunteerId).

B) **Profile & Needs Fetch**

* Policy requests `profile.get(volunteerId)` → MCP → Profile API.
* Policy requests `need.findOpen(criteria)` → MCP → Need Registry.

C) **Matching & Proposal**

* Policy runs scoring algorithm (subjects, language, availability, etc.).
* Selects best fit need.
* Emits `fulfillment.match.proposed.v1 { volunteerId, needId }`.

D) **Assignment & Confirmation**

* Auto-assign or await volunteer confirmation (configurable).
* Calls `need.assign(volunteerId, needId)` via MCP.
* Sends assignment message → `comms.send("assignment-confirmation")`.
* Optionally creates first meeting link → `meet.create()`.

E) **Finalize & Exit**

* Updates volunteer and need profile status.
* Emits:
  * `fulfillment.assigned.v1` (success)
  * or `fulfillment.declined.v1` (if volunteer rejects)
  * or `fulfillment.failed.v1` (if no match found).

***

#### Capabilities

* **Agentic Layer**: orchestrates matching, decisions, and event lifecycle.
* **MCP Client/Server**: runs tool intents (profile, need registry, comms, meeting).
* **Services**: Profile API, Need API, Comms, Meeting Scheduler.

***

#### Failure / Edge Handling

**will be added soon**
