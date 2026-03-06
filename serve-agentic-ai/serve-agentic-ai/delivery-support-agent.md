# Delivery Support Agent

Delivery Support Agent MVP = fetch today's scheduled sessions and send reminder notifications to the volunteer and need coordinator to ensure the class happens as planned.

```
Trigger: scheduled cron run every morning
        ↓
Orchestrator invokes Delivery Support Agent
        ↓
Fetch all deliverables scheduled for today
        ↓
Validate deliverable details (volunteer, school, time)
        ↓
Send reminder message to Volunteer
        ↓
Send reminder message to Need Coordinator
        ↓
Record notification status / telemetry
        ↓
Complete activity
```
