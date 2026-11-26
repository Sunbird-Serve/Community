# Solution Architecture - Vishwas Enhancements

<figure><img src="../../.gitbook/assets/Serve Vishwas Credential Architecture.png" alt=""><figcaption></figcaption></figure>

The Serve Solution Architecture has been enhanced to incorporate **Vishwas, the trust layer of the Volunteering DPI**. These enhancements enable trusted identity verification, consent-based information sharing, claim attestation and the issuance of portable, verifiable credentials across the volunteering ecosystem.

The existing microservice architecture remains unchanged, with additional capabilities introduced within the respective building blocks.

#### **1. Serve - Reference Solution**

**Volunteer Credential Wallet**

A digital wallet that enables volunteers to hold, view, manage and share their verifiable credentials. A volunteer can build a collection of credentials throughout their volunteering journey, including:

* Identity verification
* Skills and competencies
* Volunteering hours and contributions
* Training and certifications
* Volunteering experience

Volunteers can selectively present relevant credentials to other organisations, enabling portability of trust across volunteering networks.

#### **2. Serve RC - Registry and Credential Infrastructure**

Serve RC is extended to support the foundational data and credential infrastructure required for Vishwas.

| Building block               | Description                                                                                        |
| ---------------------------- | -------------------------------------------------------------------------------------------------- |
| Consent Records              | Maintains records of consent granted, modified or withdrawn by individuals and organisations.      |
| Claims & Attestations        | Stores claims made by volunteers and corresponding attestations, evidence and assessment outcomes. |
| Volunteer Credentials        | Maintains issued credential records and associated metadata.                                       |
| Credential Schemas           | Defines standardised structures for different types of volunteering credentials.                   |
| Signing, Revocation & Status | Supports cryptographic signing, credential authenticity, validity and revocation management.       |

The credential infrastructure is proposed to leverage Sunbird RC, subject to validation of its supported capabilities and standards.

#### **3. Serve Volunteering (Existing Microservice) - Trust Management**

Serve Volunteering manages the business workflows associated with establishing and maintaining trust.

| **Component**        | **Description**                                                                                                                        |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Consent Management   | Manages consent requests, permissions, withdrawal and information-sharing policies.                                                    |
| Claims & Attestation | Enables volunteers to make claims about their identity, skills and experience, and authorised organisations to assess and attest them. |
| Credentialing        | Manages credential eligibility, issuance triggers, issuer authorisation and credential lifecycle.                                      |

Credentialing is designed as a **generic, schema-driven capability**, allowing new credential types to be introduced without significant changes to the underlying application.

#### **4. Serve Hub - Verification and Integration**

Serve Hub acts as the integration layer connecting Serve with external systems, verification providers and volunteering networks.

| **Components**                 | **Description**                                                                                                                                                       |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agency Access                  | Enables organisations with their own applications and data to access Serve capabilities through standardised interfaces.                                              |
| Identity & Agency Verification | Integrates with trusted external verification sources, such as Aadhaar-based identity verification and NGO Darpan, subject to applicable permissions and regulations. |
| Credential Verification        | Enables verification of digitally issued credentials, including authenticity, issuer trust, validity and revocation status.                                           |
| Network Interoperability       | Provides the foundation for future interoperability between independent volunteering networks through standardised protocols.                                         |

#### **5. Serve Fulfil and Serve Need**

No structural changes are introduced to these microservices.

Serve Fulfil acts as a source of contribution data, such as completed volunteering engagements, sessions delivered and volunteering hours, which can subsequently be used for credential issuance.

Serve Need can consume verified claims and credentials to support eligibility checks and need-specific volunteer requirements.

### **Credential Trust Model**

The architecture adopts the Issuer–Holder–Verifier model, enabling trust to extend beyond a single platform or organisation.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

### **Architectural Outcome**

With these enhancements, Serve evolves from a volunteering management platform into an infrastructure that enables **portable, verifiable and interoperable trust**.

Volunteers can carry their verified identity, skills, experience and contributions across organisations, while organisations can establish trust without necessarily repeating the entire verification and assessment process.

The architecture maintains a clear separation between business workflows, registry and credential infrastructure, external verification and volunteer-facing experiences, enabling Vishwas to evolve independently while supporting the larger vision of the Volunteering DPI.
