# Agency Management

To facilitate seamless integration and efficient communication, we have curated a comprehensive collection of APIs for Agency Management Service.&#x20;

### Create Agency

* This API is used to create an agency profile by providing the necessary details about the agency, including its name, description, established date, contact details, agency type, and website.
* Request:
  * Method: `POST`
  * Endpoint: `https://domain:port/api/serve-volunteer/agency/v1/create`
  * Headers:
    * `Content-Type: application/json`
  * Body:
    * The request body should include the agency profile information structured according to the provided JSON schema.
    * The `Agency` object contains properties representing the agency's details, including `name`, `description`, `establishedDate`, `contactDetails`, `agencyType`, and `website`.
    * The `ContactDetails` object represents the contact details of the agency, including `email`, `mobile`, and `address`.
    * The `Address` object represents the address details of the agency, including `plot`, `street`, `landmark`, `locality`, `state`, `district`, `village`, and `pincode`.
    * Ensure that the request body is formatted as valid JSON and sent with the `Content-Type` header set to `application/json`.
* Response:
  * The response will provide information about the created agency profile, such as a unique `agencyId` to identify the profile and a success message indicating the completion of the creation process.

#### cURL

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.agency.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "Agency": {
        "name": "Example Agency",
        "description": "This is an example agency.",
        "establishedDate": "2023-06-16",
        "contactDetails": {
          "email": "agency@example.com",
          "mobile": "1234567890",
          "address": {
            "plot": "25",
            "street": "Main Street",
            "landmark": "City Center",
            "locality": "Saket",
            "state": "Delhi",
            "district": "South Delhi",
            "village": "New Delhi",
            "pincode": "110001"
          }
        },
        "agencyType": "Need Agency",
        "website": "https://www.exampleagency.com"
      }
    }
  }' \
  https://domain:port/api/serve-agency/agency/v1/create

```

#### Example Response

```json
{
  "id": "api.serve-volunteer.agency.create",
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
    "Agency": {
        "id":"guidag67"
        "name": "Example Agency",
        "description": "This is an example agency.",
        "establishedDate": "2023-06-16",
        "contactDetails": {
          "email": "agency@example.com",
          "mobile": "1234567890",
          "address": {
            "plot": "25",
            "street": "Main Street",
            "landmark": "City Center",
            "locality": "Saket",
            "state": "Delhi",
            "district": "South Delhi",
            "village": "New Delhi",
            "pincode": "110001"
          }
        },
        "agencyType": "Need Agency",
        "website": "https://www.exampleagency.com"
      }
  }
}
```

### Retrieve Agency

```json
curl -X GET \
  -H "Content-Type: application/json" \
  https://domain:port/api/serve-volunteer/agency/v1/{agencyId}
```

### Update Agency

```json
curl -X PUT \
  -H "Content-Type: application/json" \
  -d '{
    "id": "api.serve-volunteer.agency.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "agencyId": "{agencyId}",
      "Agency": {
        "name": "Updated Agency Name"
      }
    }
  }' \
  https://domain:port/api/serve-volunteer/agency/v1/update
```
