---
description: full end-to-end behaviour inside the SERVE Agentic-AI stack
---

# Volunteer-Coordinator Agentic Orchestrator

#### Mission & Scope

> Own the **volunteer** from the instant someone registers until they are serving a confirmed deliverable.\
> Sub-goals = greet ➜ volunteer selection discussion ➜ decision (on the outcome) ➜ match ➜ assignment, while enforcing policy  and emitting telemetry.

***

#### Main Actors & Layers

| Layer             | Who/What participates here                                                                                                           | objects                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| **UI**            | Volunteer mobile / web screen                                                                                                        | Register form                                                                                 |
| **Agentic AI**    | <p><strong>Volunteer-Coordinator Orchestrator</strong> ← orchestrates<br>• WelcomeAgent<br>• SelectionAgent<br>• AssignmentAgent</p> | –                                                                                             |
| **MCP Client**    | Prompt-Handler · Agent-Router · Tool-Invoker · Context-Mgr                                                                           | intent JSON, tool payload                                                                     |
| **MCP Server**    | Validator · Payload Builder · Response Interpreter                                                                                   | `WhatsAppSend`, `Calendar.createEvent`, `FulfillmentService.assign, NeedService.deliverables` |
| **Tool Adapters** | WhatsApp/Twilio · Email · Calendar · VolunteerService · NeedService · FulfillService, Firebase                                       | external APIs                                                                                 |
| **Context Store** | Redis / Postgres / VectorDB                                                                                                          | `volunteerState`, interview scores                                                            |
| **Telemetry**     | Event emitter                                                                                                                        | `welcome_sent`, `assignment_success`                                                          |
| **Team**          | Slack / email alerts                                                                                                                 | manual follow-up                                                                              |

#### Detailed Walk-through

<table><thead><tr><th width="83.6666259765625">#</th><th width="207.66668701171875">Phase &#x26; Action (Orchestrator view)</th><th>Assistant Agent</th><th>MCP Tool calls</th><th>Key Decisions / Errors</th></tr></thead><tbody><tr><td><strong>1</strong></td><td><strong>Registration event</strong> (<code>volunteer.registered</code>) arrives from VolunteeringService.</td><td>—</td><td>—</td><td>Orchestrator sets state = <code>NEW</code>.</td></tr><tr><td><strong>2</strong></td><td>Send personal welcome &#x26; ask for 15-min chat.</td><td><strong>WelcomeAgent</strong></td><td><code>WhatsAppSend</code> (primary) → fallback <code>EmailSend</code></td><td>2 × 24 h retry policy.</td></tr><tr><td><strong>3</strong></td><td><strong>Decision A</strong> – Did we get a reply?</td><td>Orchestrator</td><td>timer events from Context Store</td><td>On 3rd failure ➜ <code>ESCALATE</code> </td></tr><tr><td><strong>4</strong></td><td>Parse reply --> extract availability slots.</td><td>WelcomeAgent (LLM)</td><td>LLM function-call</td><td>If ambiguous ➜ clarification loop (max 1).</td></tr><tr><td><strong>5</strong></td><td>Schedule interview; send calendar invite.</td><td><strong>SelectionAgent</strong></td><td><code>Calendar.createEvent</code>, <code>WhatsAppSend</code></td><td>Confirms slot to both sides.</td></tr><tr><td><strong>6</strong></td><td><strong>Decision B</strong> – Interview attended?</td><td>SelectionAgent</td><td>Context Store </td><td>No-show retried once; second miss ➜ <code>ESCALATE</code>.</td></tr><tr><td><strong>7</strong></td><td>Conduct interview, auto-score with LLM prompt; save <code>{score, recommend?}</code>.</td><td>SelectionAgent</td><td>LLM; <code>ContextStore.put</code></td><td>—</td></tr><tr><td><strong>8</strong></td><td><strong>Decision C</strong> – recommend / hold / reject.</td><td>Orchestrator</td><td>—</td><td>• reject ➜ polite exit message.<br>• hold ➜ training link &#x26; reminder.<br>• recommend ➜ next phase.</td></tr><tr><td><strong>9</strong></td><td>Fetch open needs &#x26; run matching algorithm.</td><td><strong>AssignmentAgent</strong></td><td><code>NeedService.needDiscovery</code>, Registry.UserProfile.Preference</td><td>If none fit ➜ backlog report to team.</td></tr><tr><td><strong>10</strong></td><td>Volunteer accepts.</td><td>AssignmentAgent</td><td><code>FulfillmentService.assign</code>, <code>VolunteeringService.updateStatus</code></td><td>Orchestrator marks state =<code>ASSIGNED</code>.</td></tr><tr><td><strong>11</strong></td><td>Fire cross-domain event <code>need.assigned</code>.</td><td>Orchestrator</td><td>Telemetry</td><td>Need-Coordinator Orchestrator now picks up and schedules class sessions.</td></tr></tbody></table>
