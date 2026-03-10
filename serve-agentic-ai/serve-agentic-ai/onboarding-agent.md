# Onboarding Agent

**Goal** - Discover the intent, orient them with the available nature of needs, have them sign up for the purpose behind the needs. The purpose of the needs here is enabling equitable access to quality education.&#x20;

discover their capabilities(around skills, educational qualification, work and volunteer experiences and language proficiency) to volunteer for a need and their mandatory perquisites which are legal adult and willing to give time as a volunteer without pay.&#x20;

**User details** - Men and Women who are working professionals, students, senior citizens or home makers. belong to age group of 18 to 75

**Guardrails** - Do not mark onboarding complete unless mandatory fields are captured, Do not invent or assume volunteer details, Do not repeat already confirmed questions, Do not overwhelm with too many questions in one turn, Do not continue endlessly if user clearly wants to pause, Do not promise assignment or selection at this stage, Keep responses concise and warm

**MCP Tools required -** Session tools (for fetching, creating and pausing the sessions), Firebase for auth, serve user registry, user profile registry, memory tools

#### MCP Capabilities&#x20;

* `onboarding.resume_context`: Retrieve the latest onboarding context so the agent can resume from the correct point without repeating confirmed details.
* `onboarding.start_session`: Create a new onboarding session and initialize the journey for a user with no active session.
* `onboarding.advance_state`: Progress the onboarding flow through valid state transitions in a controlled and traceable manner.
* `onboarding.extract_volunteer_profile`: Convert free-form user responses into structured volunteer profile data such as skills, qualifications, experience, languages, and availability.
* `onboarding.get_missing_fields`: Identify the remaining mandatory and optional fields required to complete onboarding.
* `onboarding.evaluate_prerequisites`: Verify whether the volunteer meets mandatory onboarding prerequisites such as legal adult status, unpaid willingness, and time commitment.
* `onboarding.evaluate_readiness`: Determine whether sufficient validated information has been collected to mark onboarding as complete and ready for handoff.
* `onboarding.save_confirmed_fields`: Persist only explicitly confirmed or clearly provided user details to maintain reliable profile data.
* `onboarding.pause_session`: Save progress and mark the onboarding journey as paused when the user wants to continue later.
* `onboarding.prepare_selection_handoff`: Build a structured handoff payload containing onboarding outcomes, eligibility, and volunteer profile details for the Selection Agent.
* `onboarding.emit_handoff_event`: Emit a standard downstream event to trigger the next workflow once onboarding is completed.
* `onboarding.log_event`: Capture onboarding telemetry and audit events such as transitions, confirmations, pauses, completion, and errors.

<br>
