# Core Verbs

#### **Need Admin (nAdmin) Actions**

<table data-header-hidden><thead><tr><th></th><th></th><th width="146"></th><th></th></tr></thead><tbody><tr><td><strong>Verb</strong></td><td><strong>Action</strong></td><td><strong>MVP Implemented?</strong></td><td><strong>Details</strong></td></tr><tr><td>REGISTER</td><td>Self</td><td>✅ Yes</td><td>Handled in the backend via APII</td></tr><tr><td>REGISTER</td><td>Schools/Agency</td><td>✅ Yes</td><td>Handled in the backend via API</td></tr><tr><td>AUTHORISE</td><td>Needs</td><td>❌ No</td><td></td></tr><tr><td>ASSIGN</td><td>Coordinators</td><td>✅ Yes</td><td>Handled in the backend via API</td></tr><tr><td>ASSIGN</td><td>Agencies</td><td>❌ No</td><td></td></tr><tr><td>DELEGATE</td><td>Actions</td><td>❌ No</td><td></td></tr><tr><td>REVIEW</td><td>Rating</td><td>❌ No</td><td></td></tr><tr><td>SHARE</td><td>Profile</td><td>❌ No</td><td></td></tr><tr><td>SHARE</td><td>Needs</td><td>❌ No</td><td></td></tr></tbody></table>

#### **Need Coordinator (nCoordinator) Actions**

<table data-header-hidden><thead><tr><th></th><th width="195"></th><th width="165"></th><th></th></tr></thead><tbody><tr><td><strong>Verb</strong></td><td><strong>Action</strong></td><td><strong>MVP Implemented?</strong></td><td><strong>Details</strong></td></tr><tr><td>REGISTER</td><td>Self</td><td>✅ Yes</td><td>Handled in the backend via API</td></tr><tr><td>ONBOARD</td><td>School/Agency</td><td>✅ Yes</td><td>Handled in the backend via API</td></tr><tr><td>RAISE</td><td>Needs</td><td>✅ Yes</td><td>Completed</td></tr><tr><td>REVIEW</td><td>Nomination</td><td>✅ Yes</td><td>Completed</td></tr><tr><td>NOTIFY</td><td>Volunteer</td><td>❌ No</td><td></td></tr><tr><td>DISCOVER</td><td>Volunteers</td><td>❌ No</td><td></td></tr><tr><td>REQUEST</td><td>A Volunteer</td><td>❌ No</td><td></td></tr><tr><td>PLAN</td><td>Need Deliverables</td><td>❌ No</td><td>To be Discussed</td></tr><tr><td>TRACK</td><td>Need Deliverables</td><td>✅ Yes</td><td>Completed</td></tr><tr><td>RATE</td><td>Volunteer</td><td>❌ No</td><td></td></tr><tr><td>RATE</td><td>Need Deliverable (criteria varies)</td><td>❌ No</td><td></td></tr><tr><td>SHARE</td><td>Needs</td><td>❌ No</td><td></td></tr></tbody></table>

#### **Volunteer Actions**

| **Verb** | **Action**                         | **MVP Implemented?** | **Details**     |
| -------- | ---------------------------------- | -------------------- | --------------- |
| REGISTER | Self                               | ✅ Yes                | Completed       |
| ONBOARD  | Volunteer                          | ❌ No                 | To be discussed |
| CLAIM    | Needs                              | ❌ No                 |                 |
| DISCOVER | Needs                              | ✅ Yes                | Completed       |
| NOMINATE | for Needs                          | ✅ Yes                | Completed       |
| CONFIRM  | Nomination                         | ❌ No                 |                 |
| VIEW     | Need Deliverables                  | ✅ Yes                | Completed       |
| DELIVER  | Need Deliverables                  | ✅ Yes                | Completed       |
| RATE     | Need Deliverable (criteria varies) | ❌ No                 |                 |
| RATE     | nCoordinator                       | ❌ No                 |                 |
| RATE     | Agency                             | ❌ No                 |                 |
| SHARE    | Profile                            | ❌ No                 |                 |
| SHARE    | Credentials                        | ❌ No                 |                 |
| SHARE    | Needs                              | ❌ No                 |                 |
| ENGAGE   | Community                          | ❌ No                 |                 |

#### **Volunteer Admin (vAdmin) Actions**

| **Verb** | **Action**    | **MVP Implemented?** | **Details**                    |
| -------- | ------------- | -------------------- | ------------------------------ |
| REGISTER | Agency        | ✅ Yes                | Handled in the backend via API |
| ASSIGN   | vCoordinators | ✅ Yes                | Handled in the backend via API |
| REVIEW   | Ratings       | ❌ No                 |                                |
| ISSUE    | Credentials   | ❌ No                 |                                |
| SHARE    | Profile       | ❌ No                 |                                |
| SHARE    | Needs         | ❌ No                 |                                |

#### **Volunteer Coordinator (vCoordinator) Actions**

| **Verb** | **Action** | **MVP Implemented?** | **Details**                    |
| -------- | ---------- | -------------------- | ------------------------------ |
| REGISTER | Self       | ✅ Yes                | Handled in the backend via API |
| ONBOARD  | Volunteer  | ❌ No                 | To be discussed                |
| ATTEST   | Volunteers | ❌ No                 |                                |
| SHARE    | Needs      | ❌ No                 |                                |

#### **System Actions**

| **Verb** | **Action**   | **MVP Implemented?** |
| -------- | ------------ | -------------------- |
| ATTEST   | Claims       | ❌ No                 |
| PUBLISH  | Needs        | ✅ Yes                |
| CREDIT   | Time         | ❌ No                 |
| ISSUE    | Credentials  | ❌ No                 |
| PUBLISH  | Leaderboards | ❌ No                 |
| PUBLISH  | Usage        | ❌ No                 |

#### **Super Admin Actions**

| **Verb**  | **Action** | **MVP Implemented?** |
| --------- | ---------- | -------------------- |
| ATTEST    | Agency     | ❌ No                 |
| AUTHORISE | Admins     | ❌ No                 |
