# Need Agent

**Goal**\
Validate and work with the need coordinator to capture and validate a need, convert it into a complete and approval-ready requirement, obtain or track Need Admin approval, and then determine whether the need is approved for fulfillment, sent back for refinement, paused, or escalated for review.

**Question** - 1) felt that need agent should also be responsible of getting the need admin approval for the need. what do u say? It will be like this - **Validate Need Coordinator → Need Coordinator raises need → Need Agent structures it → Need Admin approves / rejects / asks refinement → Need Agent updates status → handoff downstream**

2\) Onboarding entity also will be part of Need Agent scope?

Outcomes

* drafted
* pending approval
* approved
* sent back for refinement
* paused
* rejected / not approved
* human review

```
Coordinator initiates
        ↓
[UI: Ask for phone number first]
[WhatsApp: phone number from channel automatically]
        ↓
Resolve phone number against Serve Registry
        ├─── LINKED / TRUSTED ─────────────────────────────────┐
        │    Load need coordinator profile                     │
        │    Load linked entity(s)                             │
        │    Fetch previous need context                       │
        │                                                      │
        └─── NOT LINKED / NO MATCH ────────────────────────────│
                    ↓                                          │
             Try UDISE / school name search                    │
                    ├─── Existing School found                 │
                    │    Map coordinator → school              │
                    │    Fetch previous need context ──────────│
                    │                                          │
                    └─── New School / Entity                   │
                         Capture: name, location, UDISE        │
                         Create entity in Serve Database       │
                         Map coordinator → new school ─────────┘
                                                               │
                                    ┌──────────────────────────┘
                                    ↓
                         EXISTING SCHOOL: Show previous need
                         "Last year you had English for Grades 6-8.
                          Is this continuing? Any changes?"
                         Pre-fill draft with previous data
                         
                         NEW SCHOOL: Capture fresh need
                                    ↓
                         Capture: subjects / grades / student count
                                  time slots / start date / duration
                                    ↓
                         Validate + Confirm with coordinator
                                    ↓
                         Save as PENDING_APPROVAL (human reviews)
                                    ↓
                    ┌───────────────┴───────────────────┐
                 Approved            Refinement        Paused / Rejected / Escalate
                    ↓                    ↓
          Fulfillment Handoff    Back to coordinator
```

INITIATED → CAPTURING\_PHONE → RESOLVING\_COORDINATOR → RESOLVING\_SCHOOL → CONFIRMING\_IDENTITY → DRAFTING\_NEED → PENDING\_APPROVAL → SUBMITTED

#### User scope

Users involved in the need lifecycle, including:

* need coordinators raising a new need
* need coordinators resuming an incomplete need draft
* need admins reviewing submitted needs

Needs may be:

* clearly defined
* partially formed
* incomplete
* needing approval clarification
* sent back for refinement

#### Decision / outcome logic

* **Drafting in progress**: need is being captured and is not yet complete.
* **Pending approval**: sufficient details are captured and the need has been submitted to Need Admin for review.
* **Approved**: Need Admin has approved the need and it is ready for downstream fulfillment.
* **Refinement required**: Need Admin or system validation identifies missing or unclear details that must be corrected by the need coordinator.
* **Paused**: coordinator or admin wants to continue later.
* **Rejected / not approved**: Need Admin declines the need for program, policy, or suitability reasons.
* **Human review**: contradictory, exceptional, or sensitive case requiring manual intervention.



#### Handoff logic

* Need captured and ready for approval → **Need Admin approval step**
* Approved need → **Fulfillment Agent**
* Need sent back with comments → return to **Coordinator via Need Agent** for refinement
* Coordinator pauses → pause session, resume Need later
* Clarification or informational interruption → **Helpline Agent** → return to Need flow
* Sensitive / exceptional case → **Human / Ops review**

***

#### MCP capabilities

* `need.resume_context`: Retrieve the latest need draft, requester details, approval status, and current state so the agent can continue without restarting.
* `need.start_session`: Create a new need-capture session for a coordinator raising a fresh need.
* `need.advance_state`: Progress the need journey through valid stages such as drafting, validation, approval submission, refinement, and closure.
* `need.resolve_coordinator_identity`: Validate and resolve the coordinator’s identity and linkage to the correct program or agency context.
* `need.extract_need_details`: Convert free-form coordinator responses into structured need attributes such as requirement type, beneficiary context, schedule, subject, scope, and constraints.
* `need.get_missing_fields`: Identify which mandatory fields are still missing before the need can be submitted for approval.
* `need.save_confirmed_fields`: Persist only confirmed and validated need details without assumptions.
* `need.evaluate_submission_readiness`: Assess whether the need has sufficient validated information to be sent to Need Admin for approval.
* `need.submit_for_approval`: Submit the structured need to the Need Admin approval workflow.
* `need.fetch_approval_status`: Retrieve the latest Need Admin decision or current approval state for a submitted need.
* `need.record_approval_decision`: Store the approval outcome such as approved, refinement required, rejected, or pending.
* `need.capture_refinement_feedback`: Save Need Admin comments or requested corrections so the coordinator can refine the need.
* `need.pause_session`: Save progress and mark the need journey as paused when the coordinator wants to continue later.
* `need.create_or_update_need_record`: Create a new need record or update an existing draft with the latest confirmed details.
* `need.update_need_status`: Update the need’s lifecycle status such as draft, pending approval, approved, refinement required, paused, or rejected.
* `need.prepare_fulfillment_handoff`: Build a structured handoff payload for approved needs so they can move into fulfillment.
* `need.emit_handoff_event`: Trigger the downstream workflow after approval or other major state transitions.
* `need.write_need_summary`: Generate and store a concise summary of the need, approval state, and rationale.
* `need.log_event`: Capture telemetry and audit events such as draft creation, field confirmation, approval submission, approval outcome, refinement request, pause, and handoff.
