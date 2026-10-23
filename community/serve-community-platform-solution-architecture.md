---
description: >-
  Independent Adopter Communities with Shared SSO - UP(Uttar Pradesh) Pilot and
  TG(Telangana) Expansion
---

# Serve Community Platform Solution Architecture

<figure><img src="../.gitbook/assets/mermaid-diagram (2) (1).png" alt=""><figcaption></figcaption></figure>

The diagram shows the target logical architecture. Deployment sizing, identity configuration and community access policies will be finalised during UP pilot implementation.

\*UP - UttarPradesh, \*TG - Telangana

The proposed architecture follows **Approach 1: a shared Serve ecosystem community, with independent communities for each adopter**. We will begin with UP as the pilot and extend the model based on the learning.

**1. Who participates where**

**Serveans**, at **serveans.serve.net.in**, brings together DPG contributors, anchors and adopter coordinators. It supports platform development, contribution requests, adopter discussions and learning across programs.

Individual program communities support their volunteers and coordinators:

<table data-header-hidden><thead><tr><th width="253.66668701171875">Community</th><th>Purpose</th></tr></thead><tbody><tr><td><strong>UP -community.up.serve.net.in</strong></td><td>Program announcements, volunteer and coordinator support, training discussions, coordination and shared experiences. UP will be the first pilot.</td></tr><tr><td><strong>TG -community.tg.serve.net.in</strong></td><td>The same program community model, introduced based on the learning from UP.</td></tr><tr><td><strong>Serveans - serveans.serve.net.in</strong></td><td>Ecosystem collaboration, platform, contribution requests and shared learning.</td></tr></tbody></table>

**2. How a volunteer enters**

A volunteer or coordinator opens their community through an invitation, a direct URL or a community link provided within the Serve application.

For example, a volunteer using **up.serve.net.in** opens **community.up.serve.net.in**. Discourse redirects the browser to Keycloak for authentication. If the Keycloak session is already active, the user can return to the community without entering credentials again, subject to membership and access rules.

On first entry, a linked Discourse profile is created after successful authentication, subject to the configured registration policy. Any required onboarding or membership approval still applies.

**3. Identity and access through SSO**

Keycloak provides authentication through **OpenID Connect (OIDC) SSO**, with a separate client for each Serve application and Discourse community. UP Serve already uses Keycloak; the community integrations will be configured and tested during implementation.

Each community retains its own profiles, permissions and application sessions. **Membership in UP does not automatically grant access to TG or Serveans.**

A shared login session requires a common Keycloak realm. Separate client registration alone does not establish SSO across different realms.

Before launch:

* Confirm the Keycloak realm configuration and community admission rules.
* Configure account linking for existing users to avoid duplicate accounts.
* Test first-login profile creation, role assignment, logout and access restrictions.
* Confirm the UP community’s visibility and approval policy with the program anchor.

**4. Deployment and component design**

Each community runs as an independent Discourse deployment containing:

* The web application for discussions, membership, permissions and moderation.
* PostgreSQL for community accounts, topics, posts and settings.
* Redis for caching and background job processing.
* Upload storage for attachments and images.

Each deployment maintains its own data and credentials. This allows communities to be administered, upgraded and scaled independently. For the UP pilot, a separate host is proposed to isolate resources and operational changes from Serveans.

<table data-header-hidden><thead><tr><th width="175">Component</th><th>Proposed UP implementation</th></tr></thead><tbody><tr><td><strong>DNS and HTTPS</strong></td><td>Use <strong>community.up.serve.net.in</strong>. DNS routes to the UP host, terminate TLS at the Discourse web entry point and renew certificates automatically. TG follows the same pattern at <strong>community.tg.serve.net.in</strong>.</td></tr><tr><td><strong>Discourse host</strong></td><td>Use the supported Discourse Docker deployment on a dedicated Linux VM. Start with <strong>2 vCPU, 4 GB RAM and 60 GB SSD</strong> as an initial estimate, validate against cohort size and upload limits.</td></tr><tr><td><strong>Application and jobs</strong></td><td>Run the Discourse web application and background workers within the supported deployment. Monitor job failures and queues, especially notification email delivery.</td></tr><tr><td><strong>Data</strong></td><td>PostgreSQL, Redis and persistent upload storage for UP. Do not share the Serve application database or the Serveans database. Restrict database and Redis access to the deployment.</td></tr><tr><td><strong>Email</strong></td><td>Use an SMTP provider with a distinct UP sender identity and credentials. Configure domain authentication. Validate invitations, notifications and delivery failures. Credential recovery follows Keycloak configuration. </td></tr><tr><td><strong>Backups</strong></td><td>Schedule daily backups including uploads to isolated off-host storage. Proposed retention, <strong>7 daily and 4 weekly recovery points</strong>.</td></tr></tbody></table>

**5. How the community relates to the Serve application**

The Serve application continues to manage needs, nominations, sessions, deliverables and volunteer hours. Discourse provides the space for people to communicate, receive support and learn from one another.

The initial connection consists of **navigation links and SSO**. Direct database integration and automatic synchronisation of program records are outside the initial pilot.

**6. How operations are managed**

Program anchors and moderators manage community participation and discussions. Technical owners manage hosting, security, availability, recovery and maintenance.

**Roles and responsibilities**

<table data-header-hidden><thead><tr><th width="249">Role</th><th>Responsibility</th></tr></thead><tbody><tr><td><strong>Serve ecosystem anchors</strong></td><td>Own Serveans purpose, shared collaboration spaces and adopter coordination.</td></tr><tr><td><strong>Community manager</strong></td><td>Shape the community’s purpose and structure with the program anchor, manage onboarding, content, engagement, moderator coordination and community health.</td></tr><tr><td><strong>UP moderators</strong></td><td>Handle discussions, flags, membership requests and escalation; use limited moderator rights where sufficient.</td></tr><tr><td><strong>Technical owner</strong></td><td>Manage infrastructure, SSO configuration, privileged access, secrets, upgrades, backups, incident response and costs. </td></tr><tr><td><strong>Adopter coordinators</strong></td><td>Participate across communities and curate reusable learning to Serveans with appropriate permission.</td></tr></tbody></table>

**Security and information handling**

Require MFA for privileged users, individual administrative accounts and least privilege. Restrict SSH to authorised operators and expose only required public web ports.

Keep secrets outside repositories, use separate credentials per instance and test category permissions with ordinary member accounts.

Do not post student personal information, credentials or sensitive school records. Publish community rules, a flagging route, escalation contacts and a retention policy.

Cross-post only material suitable for the destination audience. Private content and member lists are not copied by default.

**7. How we roll out**

We will first configure the UP community, integrate Keycloak SSO, establish categories and permissions, and verify login, notifications, moderation and backup recovery.

Validation will include:

* First-login profile creation and existing-account linking.
* Community membership, category permissions and access restrictions.
* SSO session and logout behaviour.
* Invitations, notification emails and mobile access.
* Moderation workflows and backup restoration.

A defined cohort of volunteers and coordinators will then be invited.

The pilot will assess participation, usefulness, moderation effort, reliability and operating cost. Those findings will guide expansion within UP and the subsequent rollout of TG and other adopter communities.

**Implementation Roadmap**

<table><thead><tr><th width="169.33331298828125">Timeline</th><th>Technical milestone</th><th>Community manager milestone</th></tr></thead><tbody><tr><td><strong>Week 1 - Define and set up</strong></td><td>Deploy UP Discourse. Configure domain, HTTPS, email and backups.</td><td>Define the community’s purpose, initial audience, priority use cases and expected outcomes with the UP team.</td></tr><tr><td><strong>Week 2 - Connect and prepare</strong></td><td>Integrate Keycloak SSO. Configure categories and permissions, test user journeys.</td><td>Finalise community structure, guidelines, welcome journey, initial content and engagement plan. Identify moderators and the pilot cohort.</td></tr><tr><td><strong>Week 3 - Launch UP pilot</strong></td><td>Complete access and recovery checks, resolve launch issues.</td><td>Invite and onboard participants, seed discussions and support moderators.</td></tr><tr><td><strong>Weeks 4–7 - Run and learn</strong></td><td>Monitor reliability, resolve issues and track operating costs.</td><td>Drive participation, gather feedback and review engagement weekly.</td></tr><tr><td><strong>Week 8 - Review and expand</strong></td><td>Refine the setup and assess TG deployment readiness.</td><td>Review pilot outcomes and recommend UP expansion and the TG community approach.</td></tr></tbody></table>
