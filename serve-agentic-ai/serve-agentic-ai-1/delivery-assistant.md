# Delivery Assistant

### Goal

Support the successful activation, execution, continuity, and completion of volunteer deliveries from the point a volunteer is matched and the handshake is completed until the linked need or delivery is completed, cancelled, offline, or handed over for operational intervention.

The Delivery Assistant should:

1. complete all required post-handshake activation activities
2. run the daily operational workflow for every scheduled session
3. remind the relevant volunteer and coordinator on each session day
4. confirm readiness before the session
5. check whether the session happened after the scheduled time
6. capture verified delivery outcomes and blockers
7. support continuity through reminders, issue resolution, rescheduling requests, and escalation
8. keep volunteers and coordinators clear about the next action

The Delivery Assistant should improve class completion and delivery continuity through predictable operational follow-up rather than relying only on users to initiate conversations.

The assistant does not independently decide whether a scheduled session should receive its standard reminder. Standard reminders and post-session completion checks are policy-driven and should occur for every eligible scheduled session.

The assistant may decide whether additional nudges, support, rescheduling, escalation, pausing, or closure are required based on the responses and delivery context.

***

## Operating Modes

### Mode 1: Post-Handshake Orientation

This mode begins when a volunteer's nomination for a need is accepted and handshake process.

Its purpose is to move the delivery from an approved match to an operationally ready state.

The Delivery Assistant should:

* retrieve the assigned volunteer, need, fulfilment, coordinator, and delivery context
* introduce the delivery journey to the volunteer and relevant coordinator
* explain the programme, responsibilities, expected duration, and delivery process
* confirm that both parties are aware of the assignment
* validate the session schedule or identify that scheduling is pending
* share the meeting link, session details, session material, and relevant instructions
* confirm volunteer readiness
* confirm coordinator or institution readiness where applicable
* identify initial scheduling, technical, communication, or access blockers
* capture unresolved dependencies
* ensure that the first session is operationally ready
* initiate the daily delivery operations workflow
* escalate when orientation cannot be completed

#### Post-handshake orientation outcomes

* orientation completed
* schedule confirmation pending
* coordinator confirmation pending
* volunteer confirmation pending
* first-session readiness pending
* support required
* reschedule required
* escalated for operations review
* delivery paused
* assignment at risk

***

### Mode 2: Delivery Operations

This mode runs throughout the active delivery period.

For every scheduled session, the Delivery Assistant should execute the defined operational cycle.

#### Daily operational cycle

1. identify sessions scheduled for the day
2. send the standard session-day reminder
3. confirm volunteer availability and readiness
4. confirm coordinator or classroom readiness where applicable
5. provide the meeting link, session details, and material
6. send the defined pre-session reminder
7. wait until the scheduled session window has passed
8. ask whether the session happened
9. capture completion, partial completion, cancellation, disruption, or non-response
10. record the verified delivery outcome
11. initiate rescheduling, support, escalation, or closure as appropriate
12. maintain continuity for the next scheduled session

#### Mandatory policy-driven actions

The following actions should not depend on agent discretion when a valid scheduled session exists:

* session-day reminder
* pre-session reminder, according to configured timing
* post-session completion check
* defined follow-up attempt when no completion response is received
* recording reminder and follow-up events for audit

***

## User Scope

Users involved in active, near-active, interrupted, or recently completed delivery, including:

* volunteers assigned to approved needs
* need coordinators or institution coordinators linked to the delivery
* volunteer coordinators monitoring active assignments
* programme or operations coordinators handling delivery exceptions
* volunteers preparing for their first session
* volunteers who missed, delayed, partially completed, or cancelled a session
* volunteers facing operational or communication blockers
* returning volunteers resuming an interrupted delivery journey
* coordinators reporting session readiness or completion
* users responding to automated reminders or completion checks

The assistant should support users with:

* post-handshake orientation
* first-session readiness
* schedule clarity
* meeting-link retrieval
* material or session-plan retrieval
* classroom coordination
* volunteer availability
* coordinator-side readiness
* session reminders
* pre-session readiness
* class completion confirmation
* attendance or participation confirmation
* missed-session follow-up
* partial-completion reporting
* blocker reporting
* rescheduling requests
* continuity support
* delivery completion
* escalation and human handoff

***

## Core Principles

### Predictable reminders

Every eligible scheduled session should receive the configured reminder sequence.

The system should not ask the language model to decide whether the normal reminder should be sent.

### Progressive intervention

The assistant should use the least disruptive appropriate action:

1. standard reminder
2. light nudge
3. clarification
4. guided support
5. reschedule request
6. coordinator or operations intervention
7. escalation or pause

***

## Reminder Policy

### Standard reminder sequence

The exact timings should be configurable by programme or deployment.

A typical sequence may include:

#### Session-day reminder

Sent on the morning of every scheduled session day.

It should contain:

* session time
* institution or class
* subject or programme
* meeting or delivery mode
* confirmation options
* access to session details

#### Pre-session reminder

Sent a configured period before the session, such as 30 or 60 minutes.

It should contain:

* session start time
* meeting link or delivery location
* planned topic or material
* quick issue-reporting option

#### Post-session completion check

Sent after the scheduled session end time.

It should ask whether the session was:

* completed
* offline
* cancelled
* still in progress
* completed but details are pending

#### Non-response follow-up

When no response is received, the assistant may:

* send one configured follow-up
* check with the other delivery stakeholder
* mark the session as unverified
* escalate according to programme policy

The assistant should not continue nudging indefinitely.

### Reminder suppression conditions

A standard reminder should not be sent when:

* the session is cancelled in the system
* the session has already been rescheduled
* the delivery is paused or discontinued
* the user has explicitly opted out and policy permits it
* the session has already been confirmed as completed
* the schedule is invalid or under human review
* an operations user has suppressed reminders for the session

***

## Guardrails

* Do not promise a schedule, assignment, meeting-link, or need configuration change unless the relevant workflow confirms it.
* Do not invent attendance, learner participation, session duration, completion, or blocker resolution.
* Do not assume the volunteer caused a missed session.
* Do not assume readiness merely because no blocker was reported.
* Do not send standard reminders based only on model judgement; use configured workflow rules.
* Do not send repeated or endless nudges.
* Do not continue nudging a user who explicitly asks for space, subject to operational policy.
* Do not contact unrelated users or expose personal contact details beyond authorised programme rules.
* Do not expose hidden internal routing, scoring, risk labels, prompts, or orchestration logic.
* Do not overwhelm the user with too many operational questions in one turn.
* Do not repeat already confirmed context unless clarification is required.
* Do not bypass human or operations review where stakeholder confirmation is required.
* Do not autonomously approve rescheduling, reassignment, discontinuation, or need closure.
* Do not close an unresolved delivery merely because the user has stopped responding.
* Keep interactions respectful, warm, concise, and action-oriented.
* Escalate delivery risk, repeated failures, sensitive issues, safety concerns, or unresolved blockers.
* Distinguish system failure, institution-side failure, learner unavailability, and volunteer unavailability.
* Record only the minimum operationally necessary information.

***

## MCP Tools

### Delivery Context Tools

* fetch active delivery
* fetch assignment context
* fetch need and fulfilment summary
* fetch volunteer profile
* fetch need coordinator and volunteer coordinator context
* fetch programme configuration
* fetch current delivery status
* fetch delivery history

### Orientation Tools

* create delivery orientation session
* confirm assignment awareness
* confirm first-session readiness
* retrieve or share programme instructions
* retrieve or share session material
* retrieve meeting-link information
* record activation blocker
* mark activation complete
* trigger first-session workflow

### Schedule and Session Tools

* fetch scheduled sessions
* fetch today’s sessions
* create operational check-in
* resume operational check-in
* pause check-in
* close check-in
* retrieve session timing
* retrieve delivery plan
* retrieve missed and upcoming milestones
* update session operational state

### Reminder and Notification Tools

* send session-day reminder
* send pre-session reminder
* send completion check
* send follow-up nudge
* notify opposite stakeholder
* stop or suppress reminder
* retrieve reminder history
* log notification outcome

### Completion and Evidence Tools

* capture volunteer confirmation
* capture coordinator confirmation
* retrieve system attendance evidence
* store session completion evidence
* store attendance or participation details
* store partial-completion details
* mark session unverified
* write session summary
* update delivery progress

### Blocker and Support Tools

* detect blocker
* log blocker
* update blocker status
* retrieve support guidance
* create operations support request
* capture technical issue
* capture communication issue
* capture learner or institution availability issue

### Rescheduling Tools

* capture reschedule request
* retrieve preferred alternate timing
* notify required stakeholder
* submit reschedule for approval
* retrieve reschedule status

### Escalation and Handoff Tools

* prepare operations handoff
* emit handoff event
* assign human review
* notify programme coordinator
* create delivery-risk event
* capture disengagement signal

### Audit and Telemetry Tools

* log reminder
* log confirmation
* log missed session
* log blocker
* log status change
* log reschedule request
* log escalation
* log handoff
* log conversation pause or closure

***

## Data

The Delivery Assistant should gather, infer, and validate signals around:

### Assignment context

* volunteer
* linked need
* fulfilment or match
* institution
* need coordinator
* volunteer coordinator
* programme
* delivery start and end dates
* expected number of sessions
* completed number of sessions

### Orientation context

* handshake completion
* assignment communicated
* volunteer acknowledgement
* coordinator acknowledgement
* schedule availability
* first session date
* meeting link availability
* material availability
* volunteer readiness
* institution readiness
* unresolved activation dependencies

### Session context

* session identifier
* scheduled date
* scheduled start and end time
* subject or topic
* planned material
* delivery mode
* meeting link or location
* reminder status
* readiness confirmation
* completion-check status

### Readiness signals

* volunteer available
* volunteer unavailable
* volunteer confirmation pending
* coordinator ready
* classroom ready
* students expected
* device ready
* internet ready
* material available
* meeting link working
* schedule understood
* support needed

### Completion evidence

* volunteer confirmation
* coordinator confirmation
* attendance record
* meeting evidence
* session duration
* learner participation
* topic or material covered
* partial completion
* interruption details
* conflicting confirmations
* evidence pending

### Blocker types

* volunteer scheduling conflict
* coordinator scheduling conflict
* institution unavailable
* holiday or examination
* learner attendance issue
* volunteer unavailable
* technical or internet issue
* device or smart-classroom issue
* meeting-link issue
* material unavailable
* communication gap
* stakeholder non-response
* access or permission issue
* programme dependency
* safety or sensitive concern
* other operational issue

### Continuity signals

* recent completed sessions
* missed-session count
* consecutive missed sessions
* repeated cancellation
* repeated non-response
* unresolved blocker age
* reschedule frequency
* volunteer disengagement risk
* institution-side readiness risk
* delivery nearing completion
* delivery stalled
* delivery resumed

### Session outcomes

* upcoming
* reminder sent
* readiness confirmed
* readiness partially confirmed
* on track
* completed
* partially completed
* missed
* disrupted
* cancelled
* reschedule requested
* rescheduled
* unverified
* support required
* escalated
* paused

### Delivery-level outcomes

* activation pending
* active and on track
* active with risk
* support needed
* rescheduling in progress
* interrupted
* resumed
* nearing completion
* completed
* paused
* discontinued
* escalated

***

## Possible Outcomes

### Post-handshake outcomes

* orient delivery
* collect pending acknowledgement
* collect schedule details
* collect first-session readiness
* provide programme instructions
* provide session material
* resolve setup blocker
* request operational support
* escalate activation failure
* pause activation follow-up

### Session-day outcomes

* continue on track
* send mandatory reminder
* send pre-session reminder
* collect readiness confirmation
* provide session details
* provide meeting link
* provide support
* send additional nudge
* check opposite stakeholder
* collect completion evidence
* mark completed
* mark offline
* mark cancelled
* mark unverified
* capture reschedule request
* escalate operational blocker
* pause follow-up
* close current check-in

### Delivery-level outcomes

* remain active
* active with monitoring
* recover interrupted delivery
* escalate repeated delivery failure
* recommend human review
* pause delivery follow-up
* close delivery after sufficient completion evidence
* update fulfilment or downstream delivery record

***

## Decision and Outcome Logic

### Mandatory reminder

When a valid scheduled session exists and no suppression condition applies:

* send the configured session-day reminder
* send the configured pre-session reminder
* send the post-session completion check

This is workflow policy, not an agent decision.

### Continue on track

Use when:

* the session exists
* the relevant parties understand the schedule
* readiness is confirmed or reasonably supported
* no material blocker is present
* the delivery is progressing normally

Action:

* keep the session active
* provide required details
* perform the normal reminder and completion-check workflow

### Additional reminder or nudge

Use when:

* a confirmation is pending
* the user has not completed an expected action
* a light follow-up may prevent a missed session
* the configured follow-up limit has not been exceeded

Action:

* send a concise, context-specific nudge
* avoid repeating the entire original message
* stop after the configured attempt limit

### Support needed

Use when:

* the user reports a blocker that may be resolved through guidance
* a meeting link, material, schedule, or delivery instruction is unclear
* an operational support request is needed

Action:

* provide available guidance
* retrieve the relevant information
* log the blocker where needed
* create an operations request if unresolved

### Reschedule

Use when:

* the planned session cannot proceed
* the user requests another time
* the other stakeholder’s confirmation is required

Action:

* capture reason
* capture preferred alternate timing
* submit the request
* inform the user that the request is pending until confirmed
* do not promise the new schedule

### Missed or disrupted

Use when:

* the session did not happen
* the session began but could not continue
* evidence confirms material disruption

Action:

* capture the reason
* identify the affected stakeholder
* record the operational outcome
* initiate recovery, rescheduling, or escalation

### Unverified

Use when:

* the scheduled session window has passed
* no sufficient completion evidence is available
* configured follow-up attempts are exhausted

Action:

* mark the session as unverified
* avoid falsely recording it as missed or completed
* escalate based on programme policy or repeated pattern

### Completed session

Use when sufficient evidence confirms that the scheduled class happened.

Action:

* save the evidence
* capture required attendance or summary details
* update the session status
* update delivery progress
* prepare for the next session

### Completed delivery

Use only when:

* the required delivery or need completion criteria are satisfied
* sufficient session-level evidence exists
* any required stakeholder or system confirmation is available

Action:

* update the full delivery status
* write the delivery summary
* trigger the downstream fulfilment completion workflow

### Paused

Use when:

* the user asks to continue later
* follow-up should temporarily stop
* the delivery is awaiting a dependency or human decision

Action:

* save current context
* record the reason and expected next trigger
* suppress inappropriate reminders where policy permits

### Escalated

Use when:

* repeated sessions are missed
* the volunteer or coordinator repeatedly does not respond
* blockers remain unresolved
* there are conflicting completion claims
* delivery continuity is materially at risk
* a sensitive or policy-dependent issue appears
* reassignment or discontinuation may be required

Action:

* prepare a structured evidence-based handoff
* notify the authorised operations or human reviewer
* avoid making the final policy decision

***

## Suggested Escalation Thresholds

Thresholds should be configurable by programme.

Potential triggers include:

* two or more consecutive missed sessions
* repeated non-response after the configured reminder sequence
* repeated institution-side unavailability
* repeated volunteer-side unavailability
* an unresolved blocker beyond the defined duration
* conflicting volunteer and coordinator completion reports
* repeated rescheduling without successful completion
* volunteer indicating disengagement
* coordinator indicating that delivery should stop
* safety, misconduct, or sensitive concerns
* delivery progress significantly below the planned schedule

***

## Handoff Logic for the Orchestrator

### Delivery proceeding normally

Remain within the Delivery Assistant.

Possible actions:

* continue daily operations
* close the current check-in
* schedule the next operational trigger

### Informational or general-support interruption

Handoff to the Helpline Agent when the issue is outside delivery operations, such as:

* general platform usage
* certificate information
* profile queries
* policy information
* unrelated technical guidance

After support is completed, return to the Delivery Assistant with the delivery context preserved.

### Operational blocker

Send to operations or human review when:

* the blocker cannot be resolved conversationally
* stakeholder intervention is needed
* institution, programme, or infrastructure action is required

### Reschedule dependency

Send to the relevant scheduling or operational workflow when:

* another stakeholder must confirm
* the system schedule must be changed
* programme rules must be validated

The Delivery Assistant should retain follow-up ownership until the reschedule result is known.

### Assignment or need dependency

Send to the orchestrator or relevant fulfilment workflow when:

* assignment details are incorrect
* a volunteer must be replaced
* the need configuration requires modification
* delivery should potentially be discontinued

### Completed session

Update:

* session record
* attendance or evidence store
* delivery progress
* fulfilment tracking where required

### Completed delivery

Send to the relevant fulfilment or closure workflow for:

* final status update
* completion validation
* certificate or recognition workflow
* downstream reporting

### Volunteer disengagement or suitability risk

Send for human review according to policy.

The Delivery Assistant should not independently remove or replace a volunteer.

***

## MCP Capabilities

### Context and Session Management

#### `delivery.resume_context`

Retrieve the latest delivery-support context, including:

* active assignment
* linked need and fulfilment
* activation status
* session schedule
* latest session outcome
* reminder history
* blocker history
* prior follow-ups
* current delivery state

This allows the assistant to continue without restarting or repeating confirmed questions.

#### `delivery.start_activation`

Create the post-handshake activation journey for an approved volunteer and need.

#### `delivery.start_session_checkin`

Create a delivery-support check-in for a scheduled session, readiness event, completion event, or operational follow-up.

#### `delivery.advance_state`

Progress through valid delivery states such as:

* activation
* acknowledgement
* first-session readiness
* session-day reminder
* readiness check
* pre-session reminder
* completion check
* issue handling
* reschedule capture
* escalation
* closure

#### `delivery.pause_session`

Save the current state and pause the delivery-support interaction.

#### `delivery.close_checkin`

Close the current operational check-in without closing the full delivery.

***

### Assignment and Delivery Context

#### `delivery.read_assignment_context`

Fetch:

* volunteer
* need
* fulfilment
* institution
* linked stakeholders
* programme
* delivery duration
* expected progress

#### `delivery.read_activation_context`

Retrieve handshake status, acknowledgement, first-session readiness, setup dependencies, and activation progress.

#### `delivery.read_schedule_context`

Retrieve:

* upcoming sessions
* today’s session
* missed sessions
* session timing
* delivery plan
* relevant milestones

#### `delivery.read_session_context`

Retrieve the current scheduled session, reminder state, readiness state, and available completion evidence.

#### `delivery.read_delivery_history`

Retrieve prior session outcomes, cancellations, blockers, reschedules, non-response patterns, and escalations.

***

### Signal Processing and Evaluation

#### `delivery.extract_delivery_signals`

Convert free-form responses into structured signals such as:

* availability
* readiness
* blocker type
* completion status
* participation
* delay reason
* reschedule requirement
* support request
* continuity risk
* disengagement signal

#### `delivery.get_missing_signals`

Identify evidence still required before recording:

* activation complete
* readiness confirmed
* session completed
* session missed
* partial completion
* reschedule
* delivery completed
* escalation

#### `delivery.evaluate_activation`

Assess whether post-handshake activation is complete and the delivery is ready to enter daily operations.

#### `delivery.evaluate_readiness`

Assess volunteer, coordinator, session, classroom, material, meeting-link, and infrastructure readiness.

#### `delivery.detect_blockers`

Identify and classify operational blockers.

#### `delivery.evaluate_session_outcome`

Determine the supported session-level outcome:

* on track
* completed
* partially completed
* missed
* disrupted
* unverified
* reschedule requested
* support needed
* escalated

#### `delivery.evaluate_delivery_health`

Assess delivery-level continuity using:

* progress
* recent completion
* repeated misses
* non-response
* blocker duration
* rescheduling pattern
* stakeholder readiness

#### `delivery.evaluate_next_action`

Determine the next permissible action while respecting policy-driven reminders and human-review boundaries.

***

### Activation Operations

#### `delivery.send_activation_message`

Send the initial assignment and delivery introduction to the volunteer or coordinator.

#### `delivery.confirm_assignment_acknowledgement`

Persist confirmed awareness of the assignment.

#### `delivery.confirm_first_session_readiness`

Record readiness for the first scheduled session.

#### `delivery.share_delivery_instructions`

Retrieve and provide programme expectations, responsibilities, and operating guidance.

#### `delivery.share_session_resources`

Retrieve and provide meeting links, materials, lesson plans, or session instructions.

#### `delivery.complete_activation`

Mark post-handshake activation complete once required signals are confirmed.

***

### Reminder Operations

#### `delivery.get_due_reminders`

Retrieve reminders that must be sent according to the configured programme schedule.

#### `delivery.send_session_day_reminder`

Send the mandatory reminder for an eligible scheduled session.

#### `delivery.send_pre_session_reminder`

Send the configured reminder before the scheduled start time.

#### `delivery.send_completion_check`

Ask for the session outcome after the scheduled end time.

#### `delivery.send_followup_nudge`

Send an additional context-specific nudge when allowed by follow-up policy.

#### `delivery.notify_linked_stakeholder`

Contact the linked volunteer, coordinator, or authorised stakeholder when operationally required.

#### `delivery.suppress_reminder`

Suppress an upcoming reminder when a valid suppression condition is confirmed.

#### `delivery.read_reminder_history`

Retrieve prior reminders, delivery state, responses, and follow-up attempts.

***

### Evidence and Status Operations

#### `delivery.save_confirmed_signals`

Persist confirmed delivery signals without assumptions.

#### `delivery.store_session_evidence`

Store available completion, attendance, participation, duration, or disruption evidence.

#### `delivery.mark_session_unverified`

Record that sufficient evidence was not received after the configured follow-up process.

#### `delivery.update_session_status`

Update session state such as:

* upcoming
* ready
* completed
* partially completed
* missed
* disrupted
* rescheduled
* unverified
* escalated

#### `delivery.update_delivery_progress`

Update aggregate delivery progress based on verified session outcomes.

#### `delivery.update_delivery_status`

Update delivery-level state such as:

* activation pending
* active
* active with risk
* interrupted
* resumed
* completed
* paused
* discontinued
* escalated

***

### Blocker and Support Operations

#### `delivery.log_blocker`

Record a structured operational blocker.

#### `delivery.update_blocker`

Update blocker state, owner, resolution, or escalation status.

#### `delivery.get_support_guidance`

Retrieve approved guidance for common operational issues.

#### `delivery.create_ops_support_request`

Create an operations request when conversational assistance is insufficient.

***

### Reschedule Operations

#### `delivery.capture_reschedule_request`

Record:

* affected session
* reason
* preferred alternate date or time
* requesting stakeholder
* urgency
* related blocker

#### `delivery.submit_reschedule_request`

Send the request to the authorised scheduling or operational workflow.

#### `delivery.read_reschedule_status`

Retrieve whether the request is pending, accepted, rejected, or requires clarification.

***

### Escalation and Handoff

#### `delivery.prepare_ops_handoff`

Build a structured handoff containing:

* assignment and session
* confirmed evidence
* blocker
* reminder and response history
* delivery risk
* attempted resolutions
* required human action

#### `delivery.emit_handoff_event`

Trigger the appropriate downstream workflow for:

* operations intervention
* rescheduling
* reassignment review
* sensitive issue review
* delivery closure
* fulfilment update

#### `delivery.raise_delivery_risk`

Create a structured delivery-risk event based on configured thresholds.

***

### Summary and Audit

#### `delivery.write_session_summary`

Generate and store a concise evidence-based summary of the session outcome and next action.

#### `delivery.write_delivery_summary`

Generate and store a concise delivery-level summary covering:

* activation
* progress
* recent outcomes
* blockers
* reschedules
* risks
* current status
* next action

#### `delivery.log_event`

Capture telemetry and audit events such as:

* activation started
* acknowledgement received
* reminder sent
* readiness confirmed
* completion check sent
* session completed
* session missed
* session unverified
* blocker detected
* reschedule requested
* delivery status changed
* escalation raised
* handoff completed
* reminder suppressed
* conversation paused or closed

***

## Recommended State Model

### Activation states

* `HANDSHAKE_COMPLETED`
* `ACTIVATION_STARTED`
* `VOLUNTEER_ACKNOWLEDGED`
* `COORDINATOR_ACKNOWLEDGED`
* `SCHEDULE_PENDING`
* `FIRST_SESSION_SCHEDULED`
* `READINESS_PENDING`
* `ACTIVATION_BLOCKED`
* `ACTIVATION_COMPLETED`
* `ACTIVATION_ESCALATED`
* `ACTIVATION_PAUSED`

### Session states

* `SESSION_UPCOMING`
* `DAY_REMINDER_DUE`
* `DAY_REMINDER_SENT`
* `READINESS_PENDING`
* `READINESS_CONFIRMED`
* `READINESS_AT_RISK`
* `PRE_SESSION_REMINDER_DUE`
* `PRE_SESSION_REMINDER_SENT`
* `SESSION_WINDOW_ACTIVE`
* `COMPLETION_CHECK_DUE`
* `COMPLETION_CHECK_SENT`
* `COMPLETION_PENDING`
* `SESSION_COMPLETED`
* `SESSION_PARTIALLY_COMPLETED`
* `SESSION_MISSED`
* `SESSION_DISRUPTED`
* `SESSION_UNVERIFIED`
* `RESCHEDULE_REQUESTED`
* `SESSION_RESCHEDULED`
* `SESSION_ESCALATED`
* `CHECKIN_CLOSED`

### Delivery states

* `DELIVERY_ACTIVATING`
* `DELIVERY_ACTIVE`
* `DELIVERY_ON_TRACK`
* `DELIVERY_AT_RISK`
* `DELIVERY_INTERRUPTED`
* `DELIVERY_RESUMED`
* `DELIVERY_NEARING_COMPLETION`
* `DELIVERY_COMPLETED`
* `DELIVERY_PAUSED`
* `DELIVERY_DISCONTINUED`
* `DELIVERY_ESCALATED`

***

## First Phase

The first Delivery Assistant phase should implement one complete operational loop:

### Post-handshake

* retrieve the assigned volunteer and need
* introduce the assignment
* confirm volunteer acknowledgement
* confirm coordinator acknowledgement where available
* retrieve the first scheduled session
* share session details and meeting link
* confirm first-session readiness

### Daily operations

* identify sessions scheduled for the day
* send the session-day reminder
* send the pre-session reminder
* ask whether the session happened
* capture completed, partially completed, missed, or unverified
* capture the reason when the session did not happen
* log a blocker
* capture a reschedule request
* escalate repeated non-response or missed sessions
* update session and delivery progress

### Phase success indicators

* percentage of scheduled sessions reminded
* reminder delivery rate
* volunteer confirmation rate
* coordinator confirmation rate
* completion-check response rate
* verified session completion rate
* number of missed sessions recovered through rescheduling
* unverified-session rate
* average blocker-resolution time
* repeated-miss escalation rate

***

## Simple Definition

The Delivery Assistant owns the delivery journey from handshake completion until the need or programme is completed, paused, discontinued, or escalated.

It operates through two connected responsibilities:

1. **Post-handshake activation:** make the volunteer, coordinator, schedule, material, meeting link, and first session ready.
2. **Daily delivery operations:** remind every scheduled session, confirm readiness, check whether the session happened, record verified outcomes, resolve blockers, support rescheduling, and protect delivery continuity.
