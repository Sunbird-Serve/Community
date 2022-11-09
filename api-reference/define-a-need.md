# Define a Need

## Request

```
POST /api/vNeed/v1/define
```

#### Request Header

<table><thead><tr><th>Field</th><th>Type</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td><code>content-type</code></td><td>string</td><td>Set to <code>application/json</code></td><td></td></tr><tr><td><code>authorization</code></td><td>string</td><td><code>{access-token}</code></td><td></td></tr></tbody></table>

#### Path Parameters

<table><thead><tr><th>Parameter</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>needType</td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

#### Request Body Schema

<pre><code>Need{
id*	string($uuid)
name*	string
needEntity*	string
needType*	string
needDetails	needDetails{
  id*	string($uuid)
  language	string
<strong>  start_time	string
</strong>  end_time	string
  status	string
  }
}</code></pre>

#### Request Body Example

```
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Mentoring",
  "needEntity": "ADWHS School",
  "needType": "Teaching",
  "needDetails": {
    "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
    "language": "Tamil",
    "start_time": "11:30:00",
    "end_time": "12:30:00",
    "status": "Unallocated"
  }
}
```

## Response

Following response object is returned after need is created.&#x20;

```
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "",
  "needEntity": "string",
  "needType": "string",
  "needDetails": [
    "id" : "d290f1ee-6c54-4b01-90e6-d701748f0851"
  ]
  "responseCode": "OK"
}
```



<table><thead><tr><th>Code</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>200</td><td>Need created</td><td></td></tr><tr><td>400</td><td>Invalid Input</td><td></td></tr><tr><td>409</td><td>Need already exist</td><td></td></tr></tbody></table>
