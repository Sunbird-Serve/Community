# SERVE Agentic AI – High-Level Architecture

Sunbird SERVE’s Agentic AI architecture combines persona focused intelligence with a tool-execution backbone. User prompts first reach dedicated “orchestrator” AIs (for Need-, Volunteer-coordinators and Volunteers) that understand intent, manage state‐machines and call specialised helper agents. Every real world action then flows through an MCP client/server pair that validates schema-based tool calls before touching SERVE micro-services, messaging, calendar or content systems.

<figure><img src="../.gitbook/assets/AI Agent - POC-Agentic AI.drawio (1).png" alt=""><figcaption></figcaption></figure>

**UI Layer**

_Single entry point for every persona_

* Web / mobile front-end where **Need-Coordinators**, **Volunteer-Management** and **Volunteers** initiate requests (“raise a need”, “register to volunteer”, “show my class”).
* Sends raw user prompts (text, button payloads, events) to the Agentic tier.

**Agentic AI Layer**\
&#xNAN;_&#x50;ersona-specific orchestrators plus their helper agents_

| Orchestrator (≤ 1 per persona)                                                          | Assistant agents it commands                                     | Typical responsibility                                                                                              |
| --------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Volunteer-Management Orchestrator</strong><br>(<em>implemented now</em>)</p> | **Onboarding**, **Selection**, **Fulfillment**                   | Manages the volunteer funnel: greet → volunteer selection discussion → (recommend / hold) → assign to an open need. |
| <p><strong>Need-Coordinator Orchestrator</strong><br><em>TBD</em></p>                   | _Need, Nomination, Schedule, Deliverable_                        | _Will cover end-to-end need life-cycle once defined._                                                               |
| <p><strong>Volunteer-Assistant AI</strong><br><em>TBD</em></p>                          | _VolunteerAssistant, ContentAccess (VG), Chatbot for Volunteers_ | _Will provide volunteer self-service (calendar, content) and a Chatbot in a later phase._                           |
|                                                                                         |                                                                  |                                                                                                                     |

> **What an orchestrator actually does**\
> – Interprets the user’s intent, keeps a state-machine for its persona, invokes the correct assistant agent, enforces policy, logs telemetry, and decides when to escalate to a human.

_For this version of the document we detail only the **Volunteer-Management Orchestrator**; the Need-Coordinator and Volunteer-Assistant rows are placeholders and will be expanded in subsequent iterations._

#### MCP Host&#x20;

| Block                  | Key sub-components                                                               | Purpose                                                                                                                                         |
| ---------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **MCP Client**         | <p>• Prompt Handler<br>• Agent Router<br>• Tool Invoker<br>• Context Manager</p> | Takes an orchestrator’s request, decides which MCP tool to call, builds a manifest compliant payload, and keeps  memory.                        |
| **Context Store**      | Redis / Postgres / Vector DB                                                     | Holds both **session state** (active slots, retry counters) and **long term memory** (interview scores, past classes) that any agent can query. |
| **LLM (Claude / GPT)** | Prompt templates & function-call schema                                          | Performs NLP -  intent classification, slot filling, summarisation, personalised copy generation, and free-text parsing.                        |
| **Telemetry**          | Event emitter (MongoDb)                                                          | Fires structured events (e.g. `welcome_sent`, `assignment_success`) that power dashboards, alerts and analytics.                                |

**MCP Server**\
The MCP Server is the single gateway between Agentic AIs and the outside world. Every callable integration, WhatsApp, Calendar, NeedService, Vidyaganga, even internal DB , is first defined in a **Tool Manifest** (name, input-schema, auth scope, rate limits). When an MCP Client submits a tool call, the **Validator & Payload Builder** checks that the JSON matches the schema, scrubs/augments it with secure credentials, and rejects anything malformed or unauthorised. It then forwards the call to the appropriate **Tool Adapter** (REST, gRPC, SDK). The **Response Interpreter** converts each raw API reply into a normalised structure (success/err, useful fields only).&#x20;

* **Tool Manifest & Schemas** – authoritative contract for every callable tool.
* **Validator & Payload Builder** – blocks malformed or unauthorised requests.
* **Response Interpreter** – normalises raw API replies for agents.

Agents never hit external systems directly.

**Tools Adapter + Integration Layer**

Wrappers that speak the outside world’s APIs but expose the MCP schema:

| Cluster                  | Sample Tools                                               |
| ------------------------ | ---------------------------------------------------------- |
| **SERVE Micro-services** | Registry, NeedService, VolunteeringService, FulfillService |
| **Messaging**            | WhatsApp API, Twilio SMS, Email/SMTP                       |
| **Scheduling**           | Calendar API (Google / Outlook)                            |
| **Content**              | Vidyaganga repository                                      |
| **Infra & Auth**         | Firebase                                                   |
