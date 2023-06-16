---
description: API Suite for Volunteer Management
---

# Volunteer Management

To facilitate seamless integration and efficient communication, we have curated a comprehensive collection of APIs for Volunteer Management Service.&#x20;

### Create Volunteer

This API call allows you to create a new volunteer. The API call expects a JSON payload containing the details of the volunteer to be created. The payload should conform to the specified JSON schema.

The request payload includes the following information:

* "Volunteer": An object containing the volunteer details.
  * "identityDetails": An object containing the identity details of the volunteer, such as their full name, gender, date of birth, and nationality.
  * "contactDetails": An object containing the contact details of the volunteer, including their email address, mobile number, and address.
    * "email": The email address of the volunteer.
    * "mobile": The mobile number of the volunteer.
    * "address": An object containing the address details of the volunteer, such as plot number, street, landmark, locality, state, district, village, and pincode.
* "status": The status of the volunteer, which can be "Active" in this example.

The API call will create a new volunteer with the provided details and return a response indicating the success or failure of the operation.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-need.need.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      {
      "Volunteer": {
        "identityDetails": {
          "fullname": "Rajesh Kumar",
          "gender": "Male",
          "dob": "1995-06-10",
          "Nationality": "Indian"
        },
        "contactDetails": {
          "email": "rajesh@example.com",
          "mobile": "9876543210",
          "address": {
            "plot": "25",
            "street": "Gandhi Road",
            "landmark": "City Center",
            "locality": "Saket",
            "state": "Delhi",
            "district": "South Delhi",
            "village": "New Delhi",
            "pincode": "110001"
          }
        },
      "status": "Active"
  }
}

    }
  }' \
     https://localhost:port/api/serve-volunteer/volunteer/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-volunteer.volunteer.create",
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
   "Volunteer": {
      "identityDetails": {
        "fullname": "Rajesh Kumar",
        "gender": "Male",
        "dob": "1995-06-10",
        "Nationality": "Indian"
      },
      "contactDetails": {
        "email": "rajesh@example.com",
        "mobile": "9876543210",
        "address": {
          "plot": "25",
          "street": "Gandhi Road",
          "landmark": "City Center",
          "locality": "Saket",
          "state": "Delhi",
          "district": "South Delhi",
          "village": "New Delhi",
          "pincode": "110001"
        }
      },
      "status": "Active"
    }
  }
}
```

### Retrieve Volunteer

```json
curl -X GET \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.volunteer.read",
    "ver": "v1",
    "ets": 0,
    "request": {
      "filters": {
        "volunteerId": "volunteer123",
        "agencyId": "agency456"
      }
    }
  }' \
  https://localhost:port/api/serve-volunteer/volunteer/v1/read

```

### Update Volunteer

```json
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.volunteer.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "volunteerId": "volunteer123",
      "Volunteer": {
        "identityDetails": {
          "fullname": "Updated Name",
          "gender": "Male",
          "dob": "1995-06-10",
          "Nationality": "Indian"
        },
        "contactDetails": {
          "email": "updated_email@example.com",
          "mobile": "9876543210",
          "address": {
            "plot": "25",
            "street": "Updated Street",
            "landmark": "City Center",
            "locality": "Saket",
            "state": "Delhi",
            "district": "South Delhi",
            "village": "New Delhi",
            "pincode": "110001"
          }
        },
        "status": "Active"
      }
    }
  }' \
  https://localhost:port/api/serve-volunteer/volunteer/v1/update

```

### Create Volunteer Profile

This API is used to create a volunteer profile. It allows you to provide details about the volunteer, including their identity, contact information, professional details, volunteer preferences, volunteer skills, volunteer onboarding details, and agency ID.

Endpoint: `https://localhost:port/api/serve-volunteer/volunteer-profile/v1/create`

HTTP Method: POST

Request Body:

* The request should include the volunteer profile information structured according to the provided JSON schema.
* The `id`, `ver`, and `ets` fields are used for API identification and tracking purposes.
* The `VolunteerProfile` object contains various properties such as `professionalDetails`, `volunteerPreference`, `volunteerSkills`, `volunteerOnboardDetails`, and `agencyId`.
* The request should be sent with the `Content-Type` header set to `application/json`.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.volunteer-profile.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      {
      "VolunteerProfile": {
      "volunteerId":"guicdvol03",
      "professionalDetails": {
        "qualification": "Graduate",
        "organisation": "ABC Company",
        "employmentStatus": "Full Time",
        "yearsOfExperience": "5"
      },
      "volunteerPreference": {
        "language": ["English", "Spanish"],
        "dayPreferred": ["Monday", "Wednesday"],
        "timePreferred": ["Morning", "Afternoon"],
        "interestAreas": ["Education", "Environment"]
      },
      "volunteerSkills": {
        "skills": [
          {
            "skillName": "Communication",
            "skillLevel": "Advanced"
          },
          {
            "skillName": "Problem Solving",
            "skillLevel": "Intermediate"
          }
        ]
      },
      "volunteerOnboardDetails": {
        "onboardStatus": [
          {
            "onboardStep": "Self Evaluation",
            "status": "Completed"
          },
          {
            "onboardStep": "Selection Discussion",
            "status": "In Progress"
          }
        ],
        "refreshPeriod": "6 months",
        "profileCompletion": "80%"
      },
      "agencyId": "ag-ency123"
    }

    }
  }' \
     https://localhost:port/api/serve-volunteer/volunteer-profile/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-volunteer.volunteer-profile.create",
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
   "VolunteerProfile": {
      "volunteerId": "volunteer123",
      "agencyId": "agency123",
      "status": "Active"
    }
  }
}
```
