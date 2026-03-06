# Engagement Agent

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The **Engagement Agent** is designed as an activity driven layer that manages volunteer engagement through structured workflows. When certain events occur in the SERVE system (such as assignment completion or campaign start), the orchestrator invokes the Engagement Agent with the relevant context. Inside the agent, an **Activity Router** evaluates the trigger, volunteer status, priority rules, and cooldown conditions to decide which engagement **Activity** should run. The selected activity is then created as an instance in an **Activity Queue**, which tracks its lifecycle (pending, running, waiting for user response, completed, etc.). An **Activity Executor** processes items from the queue, interacts with the volunteer through the messaging channel, invokes required system tools (such as fetching needs or handover to another agent), and records telemetry.&#x20;

## Activity A1 - Continuity & Reassignment Activity

### Activity Name

**Active Volunteer Continuity & Reassignment**

***

#### Bucket - Active Volunteers - Not Assigned

Trigger:

* Need Fulfilled

```
Volunteer taught Grade 6 Maths
Need fulfilled
Volunteer not assigned
→ Engagement Agent triggers continuity activity
```

### Eligibility Filter

Volunteer must satisfy:

```
volunteer_status = active
current_assignment = none
not opted_out
last_assignment_end > 7 days
```

### Frequency Rules / Cooldown

To prevent over-messaging:

```
max 1 continuity outreach every 30 days
max 2 reminders per activity
```

If volunteer declines:

```
pause outreach for 60 days
```

### Workflow Steps

```
Trigger: need fulfilled
        ↓
Orchestrator invokes Engagement Agent
        ↓
Activity Router selects
        ↓
Executor sends appreciation + continuity check
        ↓
Volunteer response?
   ├── Not now → ask for when to be reminded -> pause flow → complete
   ├── Stop → opt-out → complete
   └── Yes
         ↓
Ask: same school and same batch?
   ├── Yes → handoff to Fulfilment Agent with context
   └── No
         ↓
Collect preferred days and times
         ↓
Handoff to Fulfilment Agent with context
```



## Activity A2 — Activation from Recommended Pool

Activity Name **Recommended Volunteer - Activation**

Bucket - Volunteers who were **recommended but never utilised**.

Definition example:

```
recommended = true
no nomination
no assignment
no session history
not opted out
```

### Trigger Event

This activity is **campaign-driven**.

Typical triggers:

```
VOLUNTEER_SELECTION_CAMPAIGN_COMPLETED
POST_LONG_VACATION
```

Example:

```
Large recommended pool created after selection
→ Engagement Agent activates
```

### Eligibility Filter

Volunteer must satisfy:

```
recommended = true
not nominated
not assigned
not opted_out
```

Optional:

```
last_contact > 14 days
```

***

### Frequency Rules / Cooldown

```
max 1 outreach per volunteer per 30 days
max 2 attempts per campaign
```

Stop if volunteer opts out.

### Workflow Steps

```
Trigger: campaign end / post-vacation / recommended pool activation
        ↓
Orchestrator invokes Engagement Agent
        ↓
Activity Router selects
        ↓
Executor sends activation check (opt-in message)
        ↓
Volunteer response?
   ├── Not now → ask when to remind → pause flow → complete
   ├── Stop → opt-out → complete
   └── Yes
         ↓
Handoff volunteer context to Fulfilment Agent
         ↓
Fulfilment Agent identifies suitable needs and proceeds with nomination / assignment flow
```

#### Final Structure for Engagement Agent (MVP)

```
Engagement Agent
   │
   ├── Activity A1
   │   Active Volunteer Continuity & Reassignment (Priority)
   │
   └── Activity A2
       Recommended Volunteer Activation
```



