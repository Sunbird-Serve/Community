---
description: API Suite for Need Service
---

# Need Service

To facilitate seamless integration and efficient communication, we have curated a comprehensive collection of APIs for Need Service.&#x20;

### Raise Need

This API call allows you to raise new need. A "need" represents a specific requirement or demand. The API call expects a JSON payload containing the details of the need to be created. The payload should conform to the specified JSON schema.

The request payload includes the following information:

* "name": The name or title of the need.
* "needTypeId": An identifier for the type of need.
* "status": The status of the need, which can be one of the following: "New", "Approved", "Rejected", "Nominated", "In Progress", "Closed", or "Inactive".
* "description": A description or additional details about the need.
* "userId": The identifier of the user who has raised the need.
* "entityId": The identifier of the entity associated with the need.
* "requirementId": The identifier of the requirement associated with the need.
* "taxonomyDetails": Additional details related to the taxonomy of the need, including an identifier and a taxonomy object with information.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "Need": {
        "name": "Career Mentoring",
        "needTypeId": "guidnt04",
        "status": "New",
        "description": "Career Guidance for grade 11th and 12th",
        "userId": "guidus01",
        "entityId": "guidet02",
        "requirementId": "guidnr02",
        "taxonomyDetails": {
          "id": "guidtx02",
          "taxonomy": {
            "mentoringType": "one to one",
            "mentoringEnvironment": "virtual",
            "mentoringAreas": "Career Mentoring"
          }
        }
      }
    }
  }' \
     https://domain:port/api/serve-need/need/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-need.need.create",
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
   "Need": {
        "id": "guidn05",
        "name": "Career Mentoring",
        "needTypeId": "guidnt04",
        "status": "New",
        "description": "Career Guidance for grade 11th and 12th",
        "userId": "guidus01",
        "entityId": "guidet02",
        "requirementId": "guidnr02",
        "taxonomyDetails": {
          "id": "guidtx02",
          "taxonomy": {
            "mentoringType": "one to one",
            "mentoringEnvironment": "virtual",
            "mentoringAreas": "Career Mentoring"
          }
        }
      }
  }
}
```

### Update Need

#### cURL

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "Need": {
        "id":"guidnd02"
        "status": "Approved",
        "userId": "guidus01"
      }
    }
  }' \
     https://domain:port/api/serve-need/need/v1/update

```

#### Example Response

```json
{
  "id": "api.serve-need.need.update",
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

### Raise Need Type

This API call allows you to raise a need type. A "need type" represents a specific category or classification for a need. The API call expects a JSON payload containing the details of the need type to be created. The payload should conform to the specified JSON schema.

The request payload includes the following information:

* "name": The name or title of the need type.
* "description": A description or additional details about the need type.
* "status": The status of the need type, which can be one of the following: "New", "Approved", or "Rejected".
* "userId": The identifier of the user who raised the need type.
* "taskType": Additional details related to the type of task associated with the need type, including an identifier and a task detail. The task detail can be one of the following: "Session", "Event", or "Task".
* "taxonomyId": The identifier of the taxonomy associated with the need type.
* "onboardingStepsId": The identifier of the onboarding steps associated with the need type.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need-type.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "NeedType": {
          "name": "Mentoring",
          "description": "Mentoring online career guidance",
          "status": "New",
          "userId": "guidncd07",
          "taskType": {
            "id": "guidtt01",
            "taskDetail": "Session"
            },
          "taxonomyId": "guidtx02",
          "onboardingStepsId": "guidob01"
       }
      }
  }' \
     https://domain:port/api/serve-need/need-type/v1/create
```

#### Example Response

```json
{
  "id": "api.serve-need.need-type.create",
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
    "NeedType": {
      "id": "guidnt03",
      "name": "Mentoring",
      "description": "Mentoring online career guidance",
      "status": "New",
      "userId": "guidncd07",
      "taskType": {
        "id": "guidtt01",
        "taskDetail": "Session"
      },
      "taxonomyId": "guidtx02",
      "onboardingStepsId": "guidob01"
    }
  }
}

```

### Update Need Type

#### cURL

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-need.need-type.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "NeedType": {
        "id":"guidnt04"
        "status": "Approved",
        "userId": "guidus07"
      }
    }
  }' \
     https://domain:port/api/serve-need/need-type/v1/update

```

#### Example Response

```json
{
  "id": "api.serve-need.need-type.update",
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
