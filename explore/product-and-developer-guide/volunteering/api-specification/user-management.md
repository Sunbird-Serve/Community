---
description: API Suite for User Management
---

# User Management

To facilitate seamless integration and efficient communication, we have curated a comprehensive collection of APIs for User Management Service.&#x20;

### Create Users

This API call allows you to create a new user who can be a Volunteer, nCoordinator, nAdmin, vCoordinator and vAdmin. The API call expects a JSON payload containing the details of the user to be created. The payload should conform to the specified JSON schema.

The request payload includes the following information:

Request:

Method: `POST`

Endpoint: `https://domain:port/api/serve-volunteer/users/v1/create`

Headers:

`Content-Type: application/json`

Body:

* "Users": An object containing the user details.
  * "identityDetails": An object containing the identity details of the user, such as their full name, gender, date of birth, and nationality.
  * "contactDetails": An object containing the contact details of the user, including their email address, mobile number, and address.
    * "email": The email address of the volunteer.
    * "mobile": The mobile number of the volunteer.
    * "address": An object containing the address details of the volunteer, such as plot number, street, landmark, locality, state, district, village, and pincode.
* "status": The status of the volunteer, which can be "Active" in this example.

The API call will create a new user with the provided details and return a response indicating the success or failure of the operation.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.users.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      {
      "Users": {
        "identityDetails": {
          "fullname": "Rajesh Kumar",
          "gender": "Male",
          "dob": "1995-06-10",
          "Nationality": "Indian"
        },
        "contactDetails": {
          "email": "rajesh@example.com",
          "mobile": ["9876543210"],
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
      "status": "Active",
      "agencyId": "guidag03",
      "role": ["nCoordinator"]
  }
}

    }
  }' \
     https://domain:port/api/serve-volunteer/users/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-volunteer.users.create",
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
   "Users": {
      "identityDetails": {
        "fullname": "Rajesh Kumar",
        "gender": "Male",
        "dob": "1995-06-10",
        "Nationality": "Indian"
      },
      "contactDetails": {
        "email": "rajesh@example.com",
        "mobile": ["9876543210"],
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
      "status": "Active",
      "agencyId":"guidag03",
      "role": ["nCoordinator"]
    }
  }
}
```

### Retrieve Users

```json
curl -X GET \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-volunteer.users.read",
    "ver": "v1",
    "ets": 0,
    "request": {
      "filters": {
        "id": "guidus123",
        "agencyId": "agency456"
      }
    }
  }' \
  https://domain:port/api/serve-volunteer/users/v1/read

```

### Update Users

```json
curl -X PUT \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-volunteer.users.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "id": "guidus123",
      "Users": {
        "identityDetails": {
          "fullname": "Updated Name"
        },
        "contactDetails": {
          "email": "updated_email@example.com"
        }
      }
    }
  }' \
  https://domain:port/api/serve-volunteer/users/v1/update

```

### Create User Profile

This API is used to create a user profile. It allows you to provide details about the user, including their identity, contact information, professional details, user preferences, skills, onboarding details, and agency ID.

Endpoint: `https://domain:port/api/serve-volunteer/user-profile/v1/create`

HTTP Method: POST

Request Body:

* The request should include the volunteer profile information structured according to the provided JSON schema.
* The `id`, `ver`, and `ets` fields are used for API identification and tracking purposes.
* The `UserProfile` object contains various properties such as genericDetails, User`Preference`, `Skills`, `OnboardDetails`, and `agencyId`.
* The request should be sent with the `Content-Type` header set to `application/json`.

#### cURL

```json
  curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.user-profile.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      {
      "UserProfile": {
      "userId":"guicdvol03",
      "genericDetails": {
        "qualification": "Graduate",
        "affiliation": "ABC Company",
        "employmentStatus": "Full Time",
        "yearsOfExperience": "5"
      },
      "userPreference": {
        "language": ["English", "Spanish"],
        "dayPreferred": ["Monday", "Wednesday"],
        "timePreferred": ["Morning", "Afternoon"],
        "interestAreas": ["Education", "Environment"]
      },
      "skills": {
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
      "onboardDetails": {
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
     https://domain:port/api/serve-volunteer/user-profile/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-volunteer.user-profile.create",
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
   "UserProfile": {
      "id": "guidus123",
      "agencyId": "agency123",
      "status": "Active"
    }
  }
}
```
