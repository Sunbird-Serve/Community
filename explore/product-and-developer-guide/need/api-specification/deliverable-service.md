---
description: API Suite for Deliverable Service
---

# Deliverable Service

To facilitate seamless integration and efficient communication, we have curated a comprehensive collection of APIs for Deliverable Service.&#x20;

### Need Plan Generation

The "Need Plan" API is designed to manage and handle the generation of need plans. A need plan represents a structured plan or schedule for a specific need or requirement.

This API is called when a nominated need is approved by the nCoordinator. Need plan is generated with relevant details such as the name of the plan, a unique identifier (needId), the ID of the user assigned to the plan, the status of the plan (e.g., New, Proposed, Approved, Withdrawn), and occurrence details including the frequency, start date, end date, time slot, and days of occurrence.

Additionally, the API supports including proposed details for the need plan, such as an alternative time slot, specific days, and any additional comments. This feature is not included in the present MVP, hence the status would by default be "Approved".&#x20;

Upon successful creation of a need plan, the API will return a response with the created plan's details, including a plan ID, the provided information, timestamps for creation and updates, and the respective users who performed those actions.

Overall, the "Need Plan" API enables applications to manage and track various need plans, providing flexibility in scheduling and accommodating proposed alternatives for meeting specific requirements.

The request payload includes the following information:

* "name": The name of the need plan derived by the need.
* "needId": An identifier for the need.
* "status": The status of the need, by default "Approved"
* "assignedUserId": The identifier of the user who has been assigned to the need.
* "occurenceDetails": The occurrence details provide a structured representation of the schedule for the need plan, allowing users or systems to understand when and how frequently the plan will be executed. By specifying the start and end dates, time slot, and days, the occurrence details section offers the necessary information to effectively plan and manage the execution of the need plan.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need-plan.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "NeedPlan": {
      "name": "Plan - Science Grade 5",
      "needId": "guidn01",
      "assignedUserId": "guidfd01",
      "status": "Approved",
      "occurrenceDetails": {
          "frequency": "Weekly",
          "startDate": "2023-07-01",
          "endDate": "2023-12-31",
          "timeSlot": "10:00 AM - 11:00 AM",
          "days": ["Monday", "Wednesday", "Friday"]
       }
      }
    }
  }' \
     https://domain:port/api/serve-need/need-plan/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-need.need-plan.create",
  "ver": "v1",
  "ets": 1623867200000,
  "params": {
    "resmsgid": "c1d09b7a-1234-5678-90ab-cd1234567890",
    "msgid": null,
    "status": "successful",
    "err": null,
    "errmsg": null
  },
  "responseCode": "OK",
  "result": {
   "NeedPlan": {
        "id": "guidnp01",
        "name": "Plan - Science Grade 5",
        "needId": "guidn01",
        "assignedUserId": "guidfd01"
      }
  }
}
```

### Update Need Plan

#### cURL

```json
curl -X PUT \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need-plan.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "NeedPlan": {
        "id":"guidnp02",
        "userId": "guidus01",
        "occurrenceDetails": {
          "frequency": "Weekly",
          "startDate": "2023-07-01",
          "endDate": "2023-12-31",
          "timeSlot": "10:00 AM - 12:00 AM",
          "days": ["Monday", "Wednesday", "Friday"]
        }
      }
    }
  }' \
     https://domain:port/api/serve-need/need-plan/v1/update

```

#### Example Response

```json
{
  "id": "api.serve-need.need-plan.update",
  "ver": "v1",
  "ets": 1623867200000,
  "params": {
    "resmsgid": "c1d09b7a-1234-5678-90ab-cd1234567890",
    "msgid": null,
    "status": "successful",
    "err": null,
    "errmsg": null
  },
  "responseCode": "OK",
}
```

### Fetch Need Plan

"filters": An object containing filter criteria to narrow down the search results. In this example, the filters include:

* "needId": The identifier of the need to fetch need plan.
* "pagination": An object specifying the page number and limit for pagination. In this example, the page number is 1, and the limit is 10. This means the API will return the first 10 need plan from the result set.
* "sort": An object specifying the field and order for sorting the needs. In this example, the need plans will be sorted based on the "osCreatedAt" field in descending order.

#### cURL

```json
  curl -X GET \
     -H "Content-Type: application/json" \
     -H "authorization: bearer {access-token}" \
     -d '{
        "id": "api.serve-need.need-plan.read",
        "ver": "v1",
        "ets": 0,
        "request": {
            "filters": {
                "needId": "guidn01"
            },
            "pagination": {
                "page": 1,
                "limit": 10
            },
            "sort": {
                "field": "osCreatedAt"
            }
        }
     }' \
     https://domain:port/api/serve-need/need-plan/v1/read

```

#### Example Response

```json
{
    "id": "api.serve-need.need-plan.read",
    "params": {
        "status": "successful"
    },
    "responseCode": "OK",
    "result": {
         "NeedPlan": {
              "id":"guidnp01",
              "name": "Plan - Science Grade 5",
              "needId": "guidn01",
              "assignedUserId": "guidfd01",
              "status": "Approved",
              "occurrenceDetails": {
                  "frequency": "Weekly",
                  "startDate": "2023-07-01",
                  "endDate": "2023-12-31",
                  "timeSlot": "10:00 AM - 11:00 AM",
                  "days": ["Monday", "Wednesday", "Friday"]
               }
          },
    "ts": "2023-05-23T12:34:56Z",
    "ver": "1.0"
}
```



### Need Deliverable Generation

The "Need Deliverable" API is designed to manage and handle the generation of need deliverables like Sessions, Tasks or Events.&#x20;

This API is called when a need plan is generated and approved. Need deliverable is generated with relevant details such as taskType which could be either Sessions, Events or Tasks, the ID of the fulfillment details, the status of the deliverable(Not Started, In Progress, Reopen, Completed, Closed), and session numbers.

The request payload includes the following information:

* "needPlanId": An identifier for the need plan.
* "taskType": Deliverable type - Session, Event or Tasks
* "status": The status of the need deliverable, which would be updated by the nCoordinator.&#x20;
* "fulfillmentDetailsId": The identifier of the fulfillment details for the need.
* "sessionNumber": Number of planned sessions for the need

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need-deliverable.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "NeedDeliverable": {
      "needPlanId": "guidnp01",
      "taskType": "Sessions",
      "fulfillmentDetailsId": "guidfd01",
      "sessionNumber": "205",
      "status":"In progress"
      }
    }
  }' \
     https://domain:port/api/serve-need/need-deliverable/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-need.need-deliverable.create",
  "ver": "v1",
  "ets": 1623867200000,
  "params": {
    "resmsgid": "c1d09b7a-1234-5678-90ab-cd1234567890",
    "msgid": null,
    "status": "successful",
    "err": null,
    "errmsg": null
  },
  "responseCode": "OK",
  "result": {
   "NeedDeliverable": {
        "id": "guidnd01",
        "needPlanId": "guidnp01",
        "fulfillmentDetailsId": "guidfd01",
        "status": "In progress"
      }
  }
}
```

###
