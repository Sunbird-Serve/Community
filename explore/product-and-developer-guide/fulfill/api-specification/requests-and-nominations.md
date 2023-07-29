---
description: API Suite for handling requests and nominations
---

# Requests & Nominations

### Nominate Need

This API is called when a User nominates a need.&#x20;

* Request:
  * Method: `POST`
  * Endpoint: `https://domain:port/api/serve-fulfill/nomination/v1/create`
  * Headers:
    * `Content-Type: application/json`
  * Body:
    * `needId`: A string representing the identifier of the need for which the nomination is being made.
    * `nominationDetails`: An array of objects representing the details of each nomination. Each nomination detail object includes:
      * `nominatedUserId`: A string representing the identifier of the user being nominated.
      * `nominatedDate`: A string representing the date and time of the nomination (in ISO 8601 format).
      * `nominationStatus`: A string representing the status of the nomination. It must be one of the following values: "Nominated", "Approved", "Proposed", or "Rejected".
      * `comments`: An optional string providing additional comments or notes about the nomination.

#### cURL

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-fulfill.nomination.create",
    "ver": "v1",
    "ets": 0,
    "request": {
      "Nomination": {
	"needId": "12345",
	"nominationDetails": [
		{
		    "nominatedUserId": "user123",
		    "nominatedDate": "2023-06-25T09:00:00Z",
		    "nominationStatus": "Nominated",
		    "comments": "This is a nomination comment"
		}
	    ]
	}
    }
  }' \
  https://domain:port/api/serve-fulfill/nomination/v1/create

```

### Confirm/Reject Nomination

This API is called when nCoordinator confirms/rejects the nomination raised by the user.&#x20;

* Request:
  * Method: `POST`
  * Endpoint: `https://domain:port/api/serve-fulfill/nomination/v1/update`
  * Headers:
    * `Content-Type: application/json`
  * Body:
    * `needId`: A string representing the identifier of the need for which the nomination is being made.
    * `nominationDetails`: An array of objects representing the details of each nomination. Each nomination detail object includes:
      * `nominatedUserId`: A string representing the identifier of the user being nominated.
      * `nominatedDate`: A string representing the date and time of the nomination (in ISO 8601 format).
      * `nominationStatus`: A string representing the status of the nomination. It must be one of the following values: "Nominated", "Approved", "Proposed", or "Rejected".
      * `comments`: An optional string providing additional comments or notes about the nomination.

#### cURL

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
    "id": "api.serve-fulfill.nomination.update",
    "ver": "v1",
    "ets": 0,
    "request": {
      "Nomination": {
	"needId": "12345",
	"nominationDetails": [
		{
		    "nominatedUserId": "user123",
		    "nominatedDate": "2023-06-25T09:00:00Z",
		    "nominationStatus": "Rejected",
		    "comments": "This is a nomination comment"
		}
	    ]
	}
    }
  }' \
  https://domain:port/api/serve-fulfill/nomination/v1/update
```

## Fetch Nominations

This API is called when list of nominations need to be retrieved for a need&#x20;

*   Request:

    * Method: `GET`
    * Endpoint: `https://domain:port/api/serve-fulfill/nomination/v1/read`
    * Headers:
      * `Content-Type: application/json`

    The request payload includes the following information:

    * "filters": An object containing filter criteria to narrow down the search results. In this example, the filters include:
      * "needId": The identifier of the need to filter by.
      * "nominatedUserId": The identifier of the user associated with the nominations to filter by.
      * "nominationStatus": The status of the nominations to filter by, such as "new", "approved".
    * "sort": An object specifying the field and order for sorting the needs. In this example, the needs will be sorted based on the "osCreatedAt" field in descending order.

#### cURL

```json
curl -X GET \
  -H "Content-Type: application/json" \
  -H "authorization: bearer {access-token}" \
  -d '{
        "id": "api.serve-fulfill.nomination.read",
        "ver": "v1",
        "ets": 0,
        "request": {
            "filters": {
                "needId": 123,
                "nominatedUserId":"userId",
                "nominationStatus": "new"
            },
            "sort": {
                "field": "osCreatedAt",
                "order": "desc"
            }
        }
     }' \
  https://domain:port/api/serve-fulfill/nomination/v1/read
```
