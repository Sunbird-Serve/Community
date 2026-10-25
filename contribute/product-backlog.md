# Product Backlog and Roadmap

This page captures Serve’s capability assessment and proposed improvements. The [Release Plan](https://serve.sunbird.org/contribute/release-plan) describes the platform milestones.

**Serve Vishwas** is the proposed next milestone. The items below define its planning backlog, final inclusion and sequencing depend on prioritisation, dependencies and implementation assessment.

Current support reflects the assessment discussions and requires validation where noted.

**Roadmap**

| Milestone / phase                                     | Intended outcome                                                  | Planned scope                                                                                                                                                             |
| ----------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Vishwas - Phase 1: Reliable operations**            | Make the existing participation and delivery journey dependable   | Notifications; volunteer drop and backfill; agency registration/attestation; admin registration/authorisation; discovery, nomination and commitment; delivery and closure |
| **Vishwas - Phase 2: Configuration and trust**        | Support different volunteering contexts and trusted participation | Need and Need Type configuration; consent; claims and attestation; credentialing                                                                                          |
| **Vishwas - Phase 3: Acknowledgement and engagement** | Recognise contributions and encourage continued participation     | Broader acknowledgement; ratings and review; promotion; sharing; community access; usage publication                                                                      |
| **Sampark - Network participation**                   | Connect volunteering across platforms                             | Volunteering Fabric, protocol-based discovery and participation exchanges, interoperability pilot                                                                         |

### 1. Agency and Participant Onboarding

| **Capability**                                        | **Current support**                                                                                                              | **Planned improvement / decision**                                                                                              |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Agency registration and attestation**               | Serve Admin creates agencies through UI/API, agencies become active immediately                                                  | Enable organisation-initiated registration where needed. Define explicit attestation, including agencies created by Serve Admin |
| **Agency admin onboarding**                           | Serve Admin creates Need and Volunteer Admins through UI/API                                                                     | Retain controlled creation, assess additional registration/invitation paths and make agency authorisation explicit              |
| **Need Coordinator registration and assignment**      | Admin creation, separate registration form and school-application entry paths exist                                              | Establish consistent agency/entity assignment and authority across entry paths; verify Need Admin assignment support            |
| **Volunteer Coordinator registration and assignment** | Serve Admin creates coordinators through UI/API                                                                                  | Verify Volunteer Admin assignment support and assess self-registration or invitation requirements                               |
| **Entity onboarding**                                 | School application includes admin attestation and automatic coordinator registration                                             | Clarify registration, approval and coordinator-assignment responsibilities                                                      |
| **Volunteer registration**                            | Self-registration captures minimum details. Agency links establish association; organic registrations receive the default agency | Retain the entry paths and validate association behaviour                                                                       |
| **Volunteer profile**                                 | Skills and languages are captured                                                                                                | Assess interests and availability requirements; distinguish declared information from assessed claims                           |

### 2. Claims, Readiness and Consent

| Capability                    | Current support                                                                         | Planned improvement / decision                                                                     |
| ----------------------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Volunteer selection**       | Coordinator conducts a discussion and marks Recommended, OnHold or Inactive             | Record the assessment basis and clarify what each outcome establishes                              |
| **Claim attestation**         | Skills and languages are assessed, but individual outcomes and notes cannot be recorded | Record claim-level outcomes, assessor, date and relevant notes/evidence                            |
| **Need-specific preparation** | No preparation flow driven by Need Type                                                 | Configure applicable volunteer preparation and track completion                                    |
| **Readiness at confirmation** | No restriction based on selection outcome                                               | Permit confirmation only for volunteers marked Recommended; apply relevant need-specific checks    |
| **Consent management**        | Registry schema exists; no working functionality                                        | Review schema and implement defined purposes, capture, history, review, withdrawal and enforcement |

### 3. Need Types, Definition and Publication

| Capability                             | Current support                                                        | Planned improvement / decision                                                                                   |
| -------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Need Type management**               | Online Teaching is configured directly in DB, create/update APIs exist | Provide authorised configuration management and validate API/schema support                                      |
| **Need Type application**              | Configuration associations exist but are not automatically applied     | Apply taxonomy, deliverable type, volunteer preparation, eligibility and completion/evidence criteria            |
| **Need definition**                    | Captures name, type, entity, dates, days and time slot                 | Derive need name from taxonomy and apply type-specific information and defaults                                  |
| **Eligibility requirements**           | Removed from UI to simplify coordinator entry; schema/API need review  | Establish requirements through configuration, with simple need-level entry or overrides                          |
| **Entity association**                 | Every need belongs to an entity                                        | Retain the current rule; assess agency-level needs when a concrete use case requires them                        |
| **Need authorisation and publication** | Need Admin approval makes a need discoverable                          | Retain and validate the existing flow                                                                            |
| **Published-need changes**             | Edits become visible immediately                                       | Distinguish minor corrections from material changes; reapprove material changes and address affected commitments |

### 4. Discovery, Nomination and Commitment

| Capability                             | Current support                                                          | Planned improvement / decision                                                             |
| -------------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **Opportunity discovery**              | Public discovery supports days, time and other need details              | Retain public access and extend relevant taxonomy-based discovery                          |
| **Volunteer nomination**               | Logged-in volunteers nominate with one action                            | Retain simple nomination; assess partial participation and clarification requirements      |
| **Nomination review**                  | Need Coordinator accepts/rejects and can record a rejection reason       | Retain review responsibility and validate outcome notifications                            |
| **Volunteer confirmation**             | Acceptance notifies the volunteer and automatically finalises assignment | Add explicit volunteer confirmation and Recommended-status check                           |
| **Volunteer discovery and invitation** | Not implemented                                                          | Enable Need Coordinators to discover permitted volunteer capacity and invite participation |
| **Commitment records**                 | FulfillmentDetails is created when assignment is finalised               | Assess support for explicit agreed scope, linked nomination and retained agreement history |

### 5. Delivery, Changes and Continuity

| Capability                   | Current support                                                                                                                       | Planned improvement / decision                                                                              |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Delivery-plan generation** | Sessions generated automatically from need dates, days and time slot                                                                  | Generate after explicit volunteer confirmation                                                              |
| **Session management**       | Add, cancel and reschedule actions exist; rescheduling needs more testing                                                             | Validate behaviour and define permissions and consequences                                                  |
| **Rescheduling agreement**   | Changes do not require agreement from the other side                                                                                  | Establish proposed-change and accept/decline handling, with retained history                                |
| **Additional work**          | Sessions can be added; mutual agreement is not established                                                                            | Obtain agreement before extending commitments and generating additional delivery records                    |
| **Completion recording**     | Volunteer or Need Coordinator can mark completion; no verification step                                                               | Agree reporting and verification responsibilities, then implement the chosen rule                           |
| **Progress visibility**      | Planned, completed and cancelled sessions and overall progress are visible                                                            | Retain and validate calculations                                                                            |
| **Volunteer withdrawal**     | Only Need Coordinator can drop a volunteer                                                                                            | Add volunteer-initiated withdrawal and define notice, review and continuity arrangements                    |
| **Replacement**              | Previous sessions remain with the outgoing volunteer; future sessions become PlannedPause; new records are generated for replacements | Start replacement planning after confirmation and preserve separate attribution                             |
| **Need closure**             | Automatic after sessions reach qualifying outcomes                                                                                    | Clarify final statuses and distinguish closure from full fulfilment; validate paused/replacement accounting |

### 6. Acknowledgement, Feedback and Sharing

| **Capability**               | **Current support**                     | **Planned improvement / decision**                                                            |
| ---------------------------- | --------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Volunteer time**           | One hour credited per completed session | Adopt an agreed duration basis and support relevant contribution types                        |
| **Contribution credentials** | Not implemented                         | Define issuer, eligible claims, content, issuance, correction and verification                |
| **Ratings**                  | Not implemented                         | Define criteria for volunteers, coordinators, agencies and deliverables                       |
| **Rating review**            | Not implemented                         | Provide authorised administrative review and follow-up                                        |
| **Need sharing**             | Not implemented                         | Enable shareable published-need links and actions                                             |
| **Profile sharing**          | Not implemented                         | Enable permitted sharing with clear visibility and consent                                    |
| **Credential sharing**       | Not implemented                         | Enable recipient-controlled sharing and verification                                          |
| **Community access**         | No route from the Serve application     | Provide a clear entry to the relevant community space                                         |
| **Usage publication**        | Not implemented                         | Define and publish appropriate participation and contribution measures                        |
| **Leaderboards**             | Not implemented                         | Assess suitability before defining fair measures and visibility; optional rather than assumed |

### 7. Platform Readiness

| Area                         | Planned assessment / improvement                                                              |
| ---------------------------- | --------------------------------------------------------------------------------------------- |
| **Service responsibilities** | Review ownership against the agreed Need, Volunteering and Fulfilment boundaries              |
| **Data structures and APIs** | Assess whether current structures support the agreed journey and changes                      |
| **Database evolution**       | Maintain versioned migrations and upgrade guidance                                            |
| **Release reproducibility**  | Record compatible component versions, dependencies and required configuration                 |
| **Deployment toolkit**       | Maintain installation guidance and configuration templates                                    |
| **Access and traceability**  | Validate role/agency permissions and history for sensitive actions                            |
| **Regression testing**       | Cover confirmation, configuration, schedule changes, replacement, closure and acknowledgement |

Restructuring decisions follow implementation assessment. Capabilities are not assumed to require new tables or services.

### 8. Existing Items Requiring Status Review

These items were previously recorded as ongoing or open. Their current status must be confirmed before release allocation.

| Item                         | Previous status       | Reference                                                             |
| ---------------------------- | --------------------- | --------------------------------------------------------------------- |
| Agency short-code generation | Completed             | [Platform project](https://github.com/orgs/Sunbird-Serve/projects/15) |
| Need Admin analytics         | In Progress           | [Platform project](https://github.com/orgs/Sunbird-Serve/projects/15) |
| Notification enhancements    | Open for Contribution | [Platform project](https://github.com/orgs/Sunbird-Serve/projects/15) |

### 9. Future Direction - Serve Sampark

Sampark focuses on Volunteering Fabric and network participation.

| Area                         | Direction                                                                          |
| ---------------------------- | ---------------------------------------------------------------------------------- |
| **Cross-platform discovery** | Discover needs and permitted volunteer capacity across participating platforms     |
| **Network interactions**     | Exchange requests, nominations and participation outcomes through agreed protocols |
| **Trust and consent**        | Establish authority and permitted information exchange across participants         |
| **Interoperability pilot**   | Validate a bounded journey between participating systems                           |
| **Existing experiments**     | Assess reusable Serve-X work against the evolving protocol and use cases           |

Version, scope and delivery dates remain to be determined.

### 10. Completed Work and Historical References

Earlier milestones delivered the core volunteering journey and subsequent improvements, including:

* Need creation, discovery, nomination review and delivery tracking.
* Volunteer registration, onboarding, recommendation and profiles.
* Admin capabilities, need authorisation and entity/coordinator mapping.
* CMS integration, demand/supply rules and mobile responsiveness.
* Volunteer-hour recording.
* Coordinator registration and entity onboarding.
* Duplicate-registration validation.
* Need-requirement schema and UX improvements.
* Session addition, rescheduling and link management.
* Coordinator-initiated volunteer drop.

Historical completion refers to the scope delivered at that time. Related enhancements and limitations are captured above.

Original tracking references include:

* [Initial MVP work — SV-37](https://project-sunbird.atlassian.net/browse/SV-37)
* [Platform work](https://github.com/orgs/Sunbird-Serve/projects/15)
* [Demand/supply rules](https://github.com/orgs/Sunbird-Serve/projects/18)
* [Mobile responsiveness](https://github.com/orgs/Sunbird-Serve/projects/11)
* [Volunteer hours](https://github.com/orgs/Sunbird-Serve/projects/6)
* [Need Admin capabilities](https://github.com/orgs/Sunbird-Serve/projects/20)
* [Volunteer Admin capabilities](https://github.com/orgs/Sunbird-Serve/projects/19)
* [Need authorisation and entity mapping](https://github.com/orgs/Sunbird-Serve/projects/23)
* [Coordinator entity onboarding](https://github.com/orgs/Sunbird-Serve/projects/25)



