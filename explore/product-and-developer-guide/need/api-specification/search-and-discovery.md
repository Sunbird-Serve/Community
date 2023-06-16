---
description: API Suite for Search & Discovery Service
---

# Search & Discovery

Collection of APIs for Search and Discovery Service within Serve Need microservice

### Need Discovery

This API call allows you to retrieve a list of needs based on specified filters, pagination, and sorting parameters. The API call expects a JSON payload containing the request details. The payload should include the filters, pagination, and sorting information.

The request payload includes the following information:

* "filters": An object containing filter criteria to narrow down the search results. In this example, the filters include:
  * "needTypeId": The identifier of the need type to filter by.
  * "userId": The identifier of the user associated with the needs to filter by.
  * "status": The status of the needs to filter by, such as "active".
* "pagination": An object specifying the page number and limit for pagination. In this example, the page number is 1, and the limit is 100. This means the API will return the first 100 needs from the result set.
* "sort": An object specifying the field and order for sorting the needs. In this example, the needs will be sorted based on the "osCreatedAt" field in descending order.

#### cURL

```json
  curl -X GET \
     -H "Content-Type: application/json" \
     -d '{
        "id": "api.vneed.need.read",
        "ver": "v1",
        "ets": 0,
        "request": {
            "filters": {
                "needTypeId": 123,
                "userId":"nCoord userId",
                "status": "active"
            },
            "pagination": {
                "page": 1,
                "limit": 100
            },
            "sort": {
                "field": "osCreatedAt",
                "order": "desc"
            }
        }
     }' \
     https://localhost:port/api/serve-need/need/v1/read

```

#### Example Response

```json
{
    "id": "api.serve-need.need.read",
    "params": {
        "status": "successful"
    },
    "responseCode": "OK",
    "result": {
        "Need": {
            "id": "guidn01",
            "name": "Science Grade 5",
            "description": "Science Grade 5 remote teaching",
            "status": "active",
            "userId":"guidncd08"
            "needTypeId": "guidnt01",
            "entityId":"guidet01",
            "requirementId":"guidnr01"
            "taxonomyDetails": {
                 "id": "taxonomy123",
                 "taxonomy": {
                      "Board": "CBSE",
                      "Grade": "5",
                      "Subject": "Science"
                }
        }
    },
    "ts": "2023-05-23T12:34:56Z",
    "ver": "1.0"
}
```

### Need Type Discovery

This API call allows you to retrieve a list of need types based on specified filters, pagination, and sorting parameters. The API call expects a JSON payload containing the request details. The payload should include the filters, pagination, and sorting information.

The request payload includes the following information:

* "filters": An object containing filter criteria to narrow down the search results. In this example, the filters include:
  * "status": The status of the need types to filter by, such as "active".
  * "userId": The identifier of the user associated with the need types to filter by.
* "pagination": An object specifying the page number and limit for pagination. In this example, the page number is 1, and the limit is 100. This means the API will return the first 100 need types from the result set.
* "sort": An object specifying the field and order for sorting the need types. In this example, the need types will be sorted based on the "osCreatedAt" field in descending order.

#### cURL

```json
  curl -X GET \
     -H "Content-Type: application/json" \
     -d '{
        "id": "api.serve-need.need-type.read",
        "ver": "v1",
        "ets": 0,
        "request": {
            "filters": {
                "status": "active",
                "userId": "nAdmin userId"
            },
            "pagination": {
                "page": 1,
                "limit": 100
            },
            "sort": {
                "field": "osCreatedAt",
                "order": "desc"
            }
        }
     }' \
     https://localhost:port/api/serve-need/need-type/v1/read

```

#### Example Response

```json
{
  "id": "api.serve-need.need-type.read",
  "params": {
    "status": "successful"
  },
  "responseCode": "OK",
  "result": {
    "needType": {
      "id": "guidnt01",
      "name": "Online Teaching",
      "description": "Teaching online for remote schools",
      "status": "active",
      "userId": "guidncd08"
      "taskTypeId": "guidtt01",
      "taxonomyId": "guidtx01",
      "onboardingStepsId": "guidob01",
      "requirement_id": 5
    }
  },
  "ts": "2023-05-23T12:34:56Z",
  "ver": "1.0"
}
```

### Entity Discovery

To fetch list of all active entity.&#x20;

#### cURL

```json
  curl -X GET \
     -H "Content-Type: application/json" \
     -d '{
         "id": "api.serve-need.entity.read",
         "ver": "v1",
         "ets": 0,
         "request": {
             "filters": {
                 "status": "active"
             },
             "pagination": {
                 "page": 1,
                 "limit": 100
             },
             "sort": {
                 "field": "created_at",
                 "order": "desc"
             }
         }
     }' \
     https://localhost:port/api/serve-need/entity/v1/read

```

#### Example Response

```json
{
  "id": "api.serve-need.entity.read",
  "params": {
    "status": "successful"
  },
  "responseCode": "OK",
  "result": {
    "Entity": {
      "id": "guidet01",
      "name": "Abdul Kalam Digital School",
      "contactDetails": {
        "email": "contact@akdschool.com",
        "mobile": "+91 9876543210",
        "address": {
          "plot": "123",
          "street": "Main Road",
          "landmark": "Near City Park",
          "locality": "Gandhi Nagar",
          "state": "Karnataka",
          "district": "Bangalore Urban",
          "village": "Bangalore",
          "pincode": "560001"
        }
      },
      "website": "https://www.abdulkalamschool.com",
      "category": "Educational Institute"
    }
  },
  "ts": "2023-05-23T12:34:56Z",
  "ver": "1.0"
}

```
