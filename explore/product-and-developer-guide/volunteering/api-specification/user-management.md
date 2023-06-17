# User Management

To facilitate seamless integration and efficient communication, we have curated a comprehensive collection of APIs for User Management Service.&#x20;

### Create Users

* The given request is an API call to create a user profile. It is used to provide details about a user, including their identity, contact information, agency ID, status, and role.
* Request:
  * Method: `POST`
  * Endpoint: `https://localhost:port/api/serve-volunteer/users/v1/create`
  * Headers:
    * `Content-Type: application/json`
  * Body:
    * The request body should contain the user profile information structured according to the provided JSON schema.
    * The Users object contains various properties such as identityDetails, contactDetails, agencyId, status, and role. The identityDetails object contains properties like fullname, gender, dob, and Nationality, representing the user's personal information.
    * The `ContactDetails` object represents the contact details of the user, including `email`, `mobile`, and `address`.
    * The agencyId property represents the ID of the agency associated with the user. The status property represents the user's status (e.g., Active, Inactive).The role property represents the user's role, which can be one of the following: nAdmin, nCoordinator, vAdmin, vCoordinator.&#x20;
    * The request should follow the JSON schema provided and be sent with the appropriate HTTP method (e.g., POST) to the designated endpoint.
* Response:
  * The response will provide information about the created user profile, such as a unique user`Id` to identify the profile and a success message indicating the completion of the creation process.

#### cURL

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.users.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "Users": {
          "identityDetails": {
            "fullname": "Rajesh Kumar",
            "gender": "Male",
            "dob": "1995-06-10",
            "Nationality": "Indian"
            },
          "contactDetails": {
            "email": "rajesh.kumar@example.com",
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
          "agencyId": "agency123",
          "status": "Active",
          "role": "nAdmin"
      }  
    }
  }' \
  https://localhost:port/api/serve-agency/users/v1/create

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
        "id":"guidus08"
        "name": "Rajesh Kumar",
        "role": "nAdmin"
      }
  }
}
```

### Retrieve Users

```json
curl -X GET \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.users.read",
    "ver": "v1",
    "ets": 0,
    "request": {
      "filters": {
        "id": "guidus08",
        "agencyId": "agency456"
      }
    }
  }' \
  https://localhost:port/api/serve-volunteer/users/v1/read

```

### Update Agency

```json
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.users.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "id": "{user id}",
      "Users": {
        "name": "Updated User Name"
      }
    }
  }' \
  https://localhost:port/api/serve-volunteer/users/v1/update
```
