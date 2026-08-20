# Agency Management

Agency Management defines **how organisations come into SERVE, how they are trusted, and how their admins and coordinators are set up to operate.**

An Agency represents the organisation through which Needs or Volunteers are managed.

<figure><img src="../../.gitbook/assets/ChatGPT Image Aug 20, 2026, 11_37_26 AM.png" alt=""><figcaption></figcaption></figure>

***

### 1. Agency Types

| Agency Type          | What it represents | Typical responsibility                                           |
| -------------------- | ------------------ | ---------------------------------------------------------------- |
| **Need Agency**      | Demand side        | Brings institutions/schools, raises Needs and manages fulfilment |
| **Volunteer Agency** | Supply side        | Brings Volunteers, manages onboarding and supports fulfilment    |

A real-world organisation may participate as a **Need Agency, Volunteer Agency, or both**, depending on the program.

***

### 2. Key Personas

<table><thead><tr><th width="292">Persona</th><th>Responsibility</th></tr></thead><tbody><tr><td><strong>Serve Admin</strong></td><td>Attests Agencies and enables trusted participation</td></tr><tr><td><strong>Need Agency Admin (nAdmin)</strong></td><td>Manages the Need Agency, adds Need Coordinators and authorises Needs</td></tr><tr><td><strong>Need Coordinator (nCoordinator)</strong></td><td>Onboards institutions, raises Needs and coordinates fulfilment</td></tr><tr><td><strong>Volunteer Agency Admin (vAdmin)</strong></td><td>Manages the Volunteer Agency and adds Volunteer Coordinators</td></tr><tr><td><strong>Volunteer Coordinator (vCoordinator)</strong></td><td>Onboards/manages Volunteers and supports nominations</td></tr></tbody></table>

***

### 3. Agency Setup Lifecycle

```
ADMIN REGISTERS SELF
        ↓
REGISTERS AGENCY
        ↓
SERVE ADMIN ATTESTS AGENCY
        ↓
AGENCY BECOMES ACTIVE
        ↓
COORDINATOR REGISTERS SELF
        ↓
AGENCY ADMIN ADDS / ASSIGNS COORDINATOR
        ↓
AGENCY STARTS OPERATING
```

An Agency may be registered by an authorised representative or created by Serve Admin. Actors register into SERVE first and are then assigned responsibilities within an Agency. The same basic flow applies to both Need and Volunteer Agencies.

***

### 4. Need Agency Management

```
                    NEED AGENCY
                         │
                      nAdmin
                         │
              ADD / ASSIGN COORDINATORS
                         │
                   nCoordinators
                         │
               ONBOARD INSTITUTIONS
                         │
                     RAISE NEEDS
                         │
                REVIEW / AUTHORISE
                         │
                 TRACK FULFILMENT
```

| Actor            | Key Actions                                                               |
| ---------------- | ------------------------------------------------------------------------- |
| **nAdmin**       | Manage Agency profile, add Coordinators, review and authorise Needs       |
| **nCoordinator** | Onboard institution, raise/update Need, review nomination, track delivery |

***

### 5. Volunteer Agency Management

```
                 VOLUNTEER AGENCY
                         │
                      vAdmin
                         │
              ADD / ASSIGN vCoordinators
                         │
                   vCoordinators
                         │
              SHARE REGISTRATION LINK
                         │
                 VOLUNTEERS REGISTER
                         │
               ONBOARD VOLUNTEERS
                         │
                MANAGE VOLUNTEERS
                         │
                ATTEST VOLUNTEERS
```

| Actor            | Key Actions                                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------------- |
| **vAdmin**       | View/manage Agency, add or assign vCoordinators, share Volunteer registration link and view/manage Volunteers |
| **vCoordinator** | View Agency, share Volunteer registration link, onboard/manage Volunteers and attest Volunteers               |

Once the Volunteer Agency and its Volunteers are ready, Discovery and Nomination are handled as part of the Discovery & Matching capability.

***

### 6. Core Agency Verbs

| Verb             | Meaning                                                        |
| ---------------- | -------------------------------------------------------------- |
| **REGISTER**     | Bring a person or Agency into SERVE                            |
| **ATTEST**       | Confirm that the Agency is genuine and trusted                 |
| **AUTHORISE**    | Allow a person or action to proceed                            |
| **ASSIGN / ADD** | Associate a person with an Agency and give responsibility      |
| **ONBOARD**      | Make an institution, Volunteer or participant ready to operate |
| **MANAGE**       | Maintain the Agency, people and ongoing operations             |

**REGISTER** = create identity\
**ATTEST** = establish trust\
**AUTHORISE** = allow an action\
**ASSIGN** = give responsibility

***

### 7. Simple Relationship View

```
                         SERVE
                           │
                    SERVE ADMIN
                           │
                    ATTESTS AGENCY
                           │
          ┌────────────────┴────────────────┐
          │                                 │
     NEED AGENCY                     VOLUNTEER AGENCY
          │                                 │
       nAdmin                             vAdmin
          │                                 │
   nCoordinators                    vCoordinators
          │                                 │
 Institutions / Needs                  Volunteers
```

***

### 8. What Agency Management should ensure

| Question                        | What SERVE should know       |
| ------------------------------- | ---------------------------- |
| **Who is the organisation?**    | Agency identity              |
| **Can we trust it?**            | Agency attestation           |
| **Who is responsible?**         | Agency Admin                 |
| **Who operates on the ground?** | Coordinators                 |
| **Who can do what?**            | Roles and authorised actions |

***

**Agency Management is the trust and operating layer of SERVE – it brings organisations in, establishes responsibility and enables their teams to manage Needs or Volunteers.**

### Agency Management Backlog

The required APIs and schemas are already available, the pending work is primarily to implement the corresponding UI flows for Agency Management.

#### Common / Platform-level

<table><thead><tr><th width="117.66668701171875">Priority</th><th width="267">Backlog Item</th><th>Description</th></tr></thead><tbody><tr><td>P1</td><td><strong>Agency Self Registration</strong></td><td>Allow an authorised representative to register an Agency instead of only Serve Admin creating it</td></tr><tr><td>P1</td><td><strong>Agency Attestation</strong></td><td>Serve Admin reviews and attests/activates a registered Agency</td></tr><tr><td>P1</td><td><strong>Admin Assignment</strong></td><td>Serve Admin can assign the initial nAdmin/vAdmin to an Agency</td></tr><tr><td>P1</td><td><strong>Admin Self Registration</strong></td><td>Admin can register through an Agency-specific invite/registration flow</td></tr><tr><td>P2</td><td><strong>Agency Profile Management</strong></td><td>Agency Admin can update permitted Agency profile details</td></tr><tr><td>P2</td><td><strong>Agency Status Management</strong></td><td>Active / Inactive / Suspended or equivalent basic lifecycle</td></tr><tr><td>P2</td><td><strong>Role &#x26; Agency Association</strong></td><td>Clearly maintain which user has which role under which Agency</td></tr><tr><td>P3</td><td><strong>Audit Trail</strong></td><td>Track who created, attested, assigned or changed Agency roles</td></tr></tbody></table>

***

## Volunteer Agency

#### Already available

* Serve Admin creates Volunteer Agency
* Serve Admin assigns vAdmin
* vAdmin can view Agency
* vAdmin can share Volunteer registration link
* vAdmin can view Volunteers and their details
* vCoordinator can view Agency
* vCoordinator can share Volunteer registration link
* vCoordinator can view Volunteers and their details

#### Pending backlog

<table><thead><tr><th width="134.3333740234375">Priority</th><th>Backlog Item</th><th>Description</th></tr></thead><tbody><tr><td><strong>P1</strong></td><td><strong>vAdmin Self Registration</strong></td><td>Allow vAdmin to register through an Agency-specific registration/invite flow</td></tr><tr><td><strong>P1</strong></td><td><strong>Assign vCoordinator</strong></td><td>vAdmin can assign a registered user as vCoordinator</td></tr><tr><td><strong>P1</strong></td><td><strong>vCoordinator Registration Link</strong></td><td>Generate/share Agency-specific registration link for Volunteer Coordinators</td></tr><tr><td><strong>P1</strong></td><td><strong>vCoordinator Self Registration</strong></td><td>Coordinator registers and becomes available for assignment to the Agency</td></tr><tr><td><strong>P1</strong></td><td><strong>View Coordinators</strong></td><td>vAdmin can see all vCoordinators mapped to the Agency</td></tr><tr><td><strong>P2</strong></td><td><strong>Manage Coordinators</strong></td><td>Activate/deactivate/remove a Coordinator association</td></tr><tr><td><strong>P2</strong></td><td><strong>Volunteer Onboarding Status</strong></td><td>Distinguish Registered / Onboarded / Active or equivalent</td></tr><tr><td><strong>P2</strong></td><td><strong>Recommend Volunteer</strong></td><td>vAdmin/vCoordinator can mark eligible Volunteers as <strong>Recommended</strong></td></tr><tr><td><strong>P2</strong></td><td><strong>Recommended Volunteer View</strong></td><td>Filter/view Volunteers who are recommended and ready for fulfilment</td></tr><tr><td><strong>P2</strong></td><td><strong>Volunteer Profile Management</strong></td><td>View/update allowed operational details of Volunteers</td></tr><tr><td><strong>P3</strong></td><td><strong>Bulk Volunteer Management</strong></td><td>Bulk recommend, activate, deactivate or manage Volunteers where useful</td></tr></tbody></table>

## Need Agency

#### Already available

* Serve Admin creates Need Agency
* Serve Admin assigns nAdmin
* nAdmin can view Agency
* nAdmin can assign nCoordinator, onboard Entity and map entity to nCoordinators
* nCoordinator can view Agency

#### Pending backlog

<table><thead><tr><th width="155">Priority</th><th>Backlog Item</th><th>Description</th></tr></thead><tbody><tr><td><strong>P1</strong></td><td><strong>Need Agency Self Registration</strong></td><td>Allow authorised representative to register a Need Agency</td></tr><tr><td><strong>P1</strong></td><td><strong>nAdmin Self Registration</strong></td><td>nAdmin registers through Agency-specific registration/invite</td></tr><tr><td><strong>P1</strong></td><td><strong>nCoordinator Registration Link</strong></td><td>Agency-specific invite/registration link for nCoordinators</td></tr><tr><td><strong>P1</strong></td><td><strong>nCoordinator Self Registration</strong></td><td>Coordinator registers and becomes available for Agency assignment</td></tr><tr><td><strong>P2</strong></td><td><strong>Manage Coordinators</strong></td><td>Activate/deactivate/remove Coordinator association</td></tr><tr><td><strong>P2</strong></td><td><strong>Agency Profile Management</strong></td><td>nAdmin can update operational Agency information</td></tr></tbody></table>
