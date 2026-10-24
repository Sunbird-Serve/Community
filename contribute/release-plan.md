# Release Plan

Serve’s releases represent successive platform milestones. Version tags in the official repositories identify the corresponding code baselines.

| Release           | Version               | Status           | Focus                                                                  |
| ----------------- | --------------------- | ---------------- | ---------------------------------------------------------------------- |
| **Serve Vriddhi** | **v1.0.0**            | Historical MVP   | Establish the core volunteering journey                                |
| **Serve Sangam**  | **v2.0.0**            | Current baseline | Enable agency-based participation and Keycloak authentication          |
| **Serve Vishwas** | **v3.0.0 - proposed** | Under planning   | Strengthen trust, consent, commitment and contribution acknowledgement |
| **Serve Sampark** | **To be determined**  | Future direction | Connect volunteering platforms through the Volunteering Fabric         |

### Serve Vriddhi - Growth

The first MVP established need creation, volunteer registration and onboarding, opportunity discovery, nomination review, delivery planning and contribution tracking.

Vriddhi is retained as a historical code baseline.&#x20;

### Serve Sangam - Coming Together

Sangam establishes the agency-enabled platform baseline, with Keycloak authentication, agency management and role- and agency-based participation.

It brings together the UI, Need, Volunteering and Fulfilment services. Deployments require compatible component versions, database schema and configuration.

### Serve Vishwas - Trust

Vishwas takes Serve beyond the MVP towards a configurable platform for different volunteering contexts, strengthening the journey from onboarding and discovery through commitment, delivery and acknowledgement.

Planned areas of work include:

* **Configurable volunteering:** Need Types that drive taxonomy, deliverable types, eligibility, volunteer preparation and completion criteria.
* **Participation and trust:** Clear registration, authorisation and assignment flows, volunteer claims, attestation and consent.
* **Discovery and commitment:** Need-side volunteer discovery and invitations, explicit volunteer confirmation and readiness checks.
* **Delivery and continuity:** Agreed schedule changes, volunteer withdrawal, replacement, completion verification and accurate fulfilment tracking.
* **Acknowledgement and engagement:** Contribution time, credentials, feedback, sharing and access to the community.
* **Platform readiness:** Review of service responsibilities, APIs and data structures, supported by testing, deployment guidance and versioned database changes.

These areas define the milestone’s direction. Detailed scope, sequencing and delivery dates will be agreed through the Product Backlog.

### Serve Sampark - Connection

Sampark is the proposed milestone for Volunteering Fabric and network participation.

Its direction includes discovery across participating platforms, exchange of volunteering requests and outcomes, and protocol-based interoperability supported by defined trust and consent arrangements.

Version, scope and delivery dates will be established following a scoped interoperability pilot.

### Release References

Component release notes and tags are maintained in the official repositories:

* [Serve UI](https://github.com/Sunbird-Serve/sunbird-serve-ui/releases)
* [Need](https://github.com/Sunbird-Serve/sunbird-serve-need/releases)
* [Volunteering](https://github.com/Sunbird-Serve/sunbird-serve-volunteering/releases)
* [Fulfilment](https://github.com/Sunbird-Serve/sunbird-serve-fulfill/releases)

Detailed capabilities, gaps and priorities are maintained on the **Product Backlog** page. Earlier documentation labels are historical delivery identifiers and have been superseded by this release convention.
