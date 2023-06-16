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
                "userId":"guidncd08",
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
        "need": {
            "id": "guidn01",
            "name": "Science Grade 5",
            "description": "Science Grade 5 remote teaching",
            "status": "active",
            "userId":"guidncd08"
            "needTypeId": "guidnt01",
            "entityId":"guidet01",
            "requirementId":"guidnr01"
        }
    },
    "ts": "2023-05-23T12:34:56Z",
    "ver": "1.0"
}
```
