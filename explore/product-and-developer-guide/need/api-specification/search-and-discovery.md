# Search & Discovery

Collection of APIs for Search and Discovery Service within Serve Need microservice

### Need Discovery

To fetch list of needs for a particular need type or all the need created by a particular nCoordinator or all active need.&#x20;

#### cURL

```
  curl -X POST \
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

```
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

To fetch list of need types created by a particular user (nAdmin) or all active need types.&#x20;

#### cURL

```
  curl -X POST \
     -H "Content-Type: application/json" \
     -d '{
        "id": "api.vneed.need-type.read",
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

```
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

```
  curl -X POST \
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

```
{
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
}

```
