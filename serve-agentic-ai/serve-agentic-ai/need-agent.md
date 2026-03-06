# Need Agent

Need Agent MVP = collect need requirements + raise the need

```
Trigger: Need Coordinator wants to raise a new need
        ↓
Orchestrator invokes Need Agent
        ↓
Validate: is the user the Need Coordinator for the school?
        ↓
If No → inform user they are not authorized → end flow
        ↓
If Yes
        ↓
Need Agent collects need requirements step by step
        ↓
Show summary and confirm details
        ↓
Raise need in system through MCP Tool
        ↓
Return success / error response
```

Before collecting need requirements, the Need Agent first validates whether the requesting user is the authorized Need Coordinator for the respective school. Only after successful validation does the agent proceed with collecting the required details and creating the need in the system.
