# Create a Need

## Request

```
POST /api/vRC/v1/{entity_type}/need
```

#### Request Header

<table><thead><tr><th>Field</th><th>Type</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td><code>content-type</code></td><td>string</td><td>Set to <code>application/json</code></td><td></td></tr><tr><td><code>authorization</code></td><td>string</td><td><code>{access-token}</code></td><td></td></tr></tbody></table>

#### Request Path

| Field       | Type   | Description                                                                     |
| ----------- | ------ | ------------------------------------------------------------------------------- |
| entity-type | string | The type of entity to create and for vNeed the entity type created will be Need |

#### Request Body Schema

<pre><code><strong>{
</strong>	"needType": "object",
	"properties": { "Need": { "$ref": "#/definitions/Need" } },
	"definitions": {
		"Need": {
			"$id": "#/properties/Need",
			"needEntity": "object",
			"properties": {
				"name": { "type": "string" },
				"language": { "type": "string" },
				"status": { "type": "string" },
			}
		}
	},
	// Sunbird-RC specific configuration
	"_osConfig": { 
          "systemFields": [
             "_osCreatedAt",
             "_osUpdatedAt",
             "_osCreatedBy",
             "_osUpdatedBy"
        ],
        // The following field is used to define the role who will be allowed to use the POST /api/v1/&#x3C;Schema> API
        // to create the entity. The role will be validated with jwt token passed with the API.
        // If API does not require any role validation, then it can be set to anonymous
        "roles": ["admin"],
        // The following field is used to define the role who will be allowed to use the POST /api/v1/&#x3C;Schema>/invite API
        // to invite the entity. The role will be validated with jwt token passed with the API.
        // If API does not require any role validation, then it can be set to anonymous
        "inviteRoles": ["admin"],
        ]
    }
}</code></pre>

#### Request Body Example

```
"Need": {
	  "$id": "string",
	  "needEntity": "object",
	  "properties": {
		"name": { "type": "string" },
		"language": { "type": "string" },
		"status": { "type": "string" },
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
