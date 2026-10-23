---
description: >-
  Independent Adopter Communities with Shared SSO - UP(Uttar Pradesh) Pilot and
  TG(Telangana) Expansion
---

# Serve Community Platform Solution Architecture

<figure><img src="../.gitbook/assets/mermaid-diagram (2) (1).png" alt=""><figcaption></figcaption></figure>

\*UP - UttarPradesh, \*TG - Telangana

The proposed architecture follows **Approach 1: a shared Serve ecosystem community, with independent communities for each adopter**. We will begin with UP as the pilot and extend the model based on the learning.

**1. Who participates where**

Serveans, at **serveans.serve.net.in**, brings together DPG contributors, anchors and adopter coordinators. It supports platform development, contribution requests, adopter discussions and learning across programmes.

Individual programm communities support their volunteers and coordinators:

* **UP:** community.up.serve.net.in - the first pilot.
* **TG:** community.tg.serve.net.in - planned within the same architecture.

These communities host programm announcements, volunteer support, training discussions, coordination and shared experiences.

**2. How a volunteer enters**

A volunteer or coordinator can open their community through an invitation, a direct URL or a community link provided within the Serve application.

For example, a volunteer using **up.serve.net.in** opens **community.up.serve.net.in**. The community uses Keycloak to authenticate the user. If their Keycloak session is already active, they can enter without entering credentials again, subject to community membership and access rules.

On their first visit, Discourse creates a linked community profile after successful authentication. Any required onboarding or membership approval still applies.

**3. How SSO works**

Keycloak acts as the shared identity provider. Each SERVE application and Discourse community has its own OIDC client configuration.

Keycloak handles authentication, Discourse manages the community session and permissions. **SSO provides a common login experience, while access remains specific to each community.** Membership in UP does not automatically grant membership in TG or Serveans.

The diagram represents the target architecture. UP SERVE already uses Keycloak, the community integrations will be configured and tested as part of implementation.

**4. What runs inside each community**

Each community is an independent Discourse deployment containing:

* The web application for discussions, membership, permissions and moderation.
* PostgreSQL for community accounts, topics, posts and settings.
* Redis for caching and background job processing.
* Upload storage for attachments and images.

Each deployment maintains its own data and credentials. This allows communities to be administered, upgraded and scaled independently. For the UP pilot, a separate host is proposed to isolate its resources and operational changes from Serveans.

**5. How the community relates to the Serve application**

The Serve application continues to manage needs, nominations, sessions, deliverables and volunteer hours. Discourse provides the space for people to communicate, receive support and learn from one another.

The initial connection consists of navigation links and SSO. Direct database integration and automatic synchronisation of program records are outside the initial pilot.

**6. How communities remain connected**

Adopter coordinators participate in both their program community and Serveans. They bring relevant learning, recurring challenges, platform feedback and contribution requests into the wider ecosystem.

This sharing is curated by people. Discussions and private content are not automatically copied between communities.

**7. How operations are managed**

The deployments follow common operational practices for SMTP email, backups, monitoring and upgrades. The same technical team may support them, while keeping credentials and backups isolated per instance.

Program anchors and moderators manage community participation and discussions. Technical owners manage hosting, security, availability, recovery and maintenance.

**8. How we roll out**

We will first configure the UP community, integrate Keycloak SSO, establish categories and permissions, and verify login, notifications, moderation and backup recovery. A defined cohort of volunteers and coordinators will then be invited.

The pilot will assess participation, usefulness, moderation effort, reliability and operating cost. Those findings will guide expansion within UP and the subsequent rollout of TG and other adopter communities.
