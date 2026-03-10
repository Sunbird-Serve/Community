# Selection Agent

#### Goal

Autonomously conduct the volunteer readiness evaluation by understanding the volunteer’s motivation, communication clarity, teaching readiness, commitment signals, subject and language fit, and overall suitability to serve a need. Dynamically decide the best questioning and evaluation strategy to gather sufficient evidence, continuously form and evaluate the volunteer, and determine the most appropriate outcome as recommending the volunteer for fulfillment, redirecting them to engagement for future opportunities, pausing for later continuation, or escalating for human review, while maintaining a respectful and encouraging experience.&#x20;

where should the rubric or deciding factors for the outcome be mentioned? In Goal?

#### Evaluation Rubric / Decision Factors

The Selection Agent should evaluate volunteers against the following:

* motivation and purpose alignment
* seriousness and continuity intent
* communication clarity
* language comfort and fluency
* time availability realism and consistency
* willingness to volunteer unpaid
* current readiness for active needs
* suitability for immediate fulfillment versus future engagement
* blockers, concerns, or risk signals

#### Outcome Decision Logic

* **Recommended**: strong and sufficient evidence of readiness, fit, and commitment for current needs
* **Engagement later / hold**: positive or promising signals, but insufficient current readiness, availability, or fit for immediate fulfillment
* **Not matched**: clear mismatch against current need requirements or minimum readiness expectations
* **Human review**: contradictory, sensitive, exceptional, or highly ambiguous case
* **Pause**: user explicitly asks to continue later or stops mid-evaluation

#### User scope

* Volunteers who have completed onboarding
* Returning volunteers resuming selection
* Volunteers with different experience levels:
  * experienced teachers
  * first-time volunteers
  * working professionals
  * students
  * senior citizens
  * homemakers
* Volunteers who may be:
  * highly motivated
  * uncertain
  * inconsistent
  * exploratory
  * promising but not immediately ready

#### Guardrails

* Do not recommend a volunteer without sufficient evidence
* Do not expose internal scoring, rubric, or hidden evaluation logic directly
* Do not reject harshly or in discouraging language
* Do not skip essential evaluation dimensions
* Do not repeat already confirmed context unless clarification is needed
* Do not promise assignment or placement at this stage
* Keep the interaction respectful, warm, and concise
* Escalate or hold when answers are contradictory, highly ambiguous, or insufficient
* Do not invent volunteer experience, capability, or commitment

#### MCP Tools

* Session tools
  * fetch session
  * create/resume/pause session
* Volunteer profile registry
* Onboarding summary retrieval
* Selection memory tools
* Evaluation signal / rubric storage
* Volunteer status update based on outcome

**MCP Capabilities**

* `selection.resume_context`: Retrieve the latest selection session, onboarding summary, prior evaluation signals, and current state so the agent can continue without restarting.
* `selection.start_session`: Create a new selection session for a volunteer entering readiness evaluation.
* `selection.advance_state`: Progress the selection evaluation through valid state transitions in a controlled and traceable way.
* `selection.extract_evaluation_signals`: Convert free-form volunteer responses into structured evaluation signals such as motivation, clarity, commitment, teaching readiness, subject fit, and blocker indicators.
* `selection.get_missing_evidence`: Identify which required evaluation dimensions still lack sufficient evidence for a confident outcome.
* `selection.read_onboarding_summary`: Fetch the structured onboarding outcome and volunteer profile context already captured before selection begins.
* `selection.read_profile`: Retrieve the volunteer’s current registry/profile details for evaluation continuity and validation.
* `selection.save_confirmed_signals`: Persist confirmed evaluation signals and validated evidence gathered during selection.
* `selection.evaluate_readiness`: Assess whether the available evidence is sufficient to judge the volunteer’s readiness and determine whether more probing is needed.
* `selection.evaluate_outcome`: Determine the most appropriate current outcome such as recommended, engagement later, hold, not matched, or human review based on evidence and policy.
* `selection.detect_contradictions`: Identify conflicting, inconsistent, or ambiguous signals that require clarification or escalation.
* `selection.pause_session`: Save selection progress and mark the session paused when the volunteer wants to continue later.
* `selection.prepare_fulfillment_handoff`: Build a structured handoff payload for volunteers recommended for current fulfillment.
* `selection.prepare_engagement_handoff`: Build a structured handoff payload for volunteers who are promising but better suited for future engagement.
* `selection.emit_handoff_event`: Trigger the next downstream workflow once the selection outcome is finalized.
* `selection.update_volunteer_status`: Update the volunteer’s system status according to the evaluated selection outcome.
* `selection.write_evaluation_summary`: Generate and store a concise summary of evidence, outcome, and rationale for future reference and downstream use.
* `selection.log_event`: Capture telemetry and audit events such as question progression, evidence confirmation, contradictions, pause, outcome decision, escalation, and handoff.

#### Data

The Selection Agent should gather, infer, and validate evidence around:

* motivation to volunteer
* seriousness of intent
* communication clarity
* comfort interacting with children / learners
* prior teaching, mentoring, tutoring, or volunteering experience
* subject confidence
* language comfort / fluency
* time availability consistency
* willingness to volunteer without pay
* continuity / commitment signals
* possible blockers or concerns
* suitability for current needs vs future needs
* readiness outcome:
  * recommended
  * hold or engagement later
  * not matched
  * human review

#### Handoff logic - For Orchestrator

* **Recommended** → Fulfillment Agent
* **Promising but not immediately ready** → Engagement Agent
* **Volunteer pauses / asks to continue later** → pause session, resume Selection later
* **Clarification / informational interruption** → Helpline Agent → return to Selection
* **Ambiguous / sensitive / exceptional case** → Human / Ops review
* **Insufficient evidence** → remain in Selection or move to hold state

**Memory & telemetry:** evaluation summary, signals, rationale, state transitions

