---
description: >-
  This API is associated with raising a need entity on the Sunbird Serve
  Platform
---

# Raise Need Entity

### Request

{% swagger method="post" path="" baseUrl="/api/vneed/need-entity/v1/create" summary="Raise Need Entity" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" required="true" type="string" name="content-type" %}
set to application/json
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="" required="true" %}
set to 

`Bearer {access-token}`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="title" type="string" required="true" %}
title of the need entity
{% endswagger-parameter %}

{% swagger-parameter in="body" name="description" type="string" required="true" %}
A more detailed description of the need entity
{% endswagger-parameter %}

{% swagger-parameter in="body" name="need-type" type="string" required="true" %}
type of the need
{% endswagger-parameter %}

{% swagger-parameter in="body" name="location" type="string" required="true" %}
location where the need entity is situated
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="string" required="false" %}
status of the need entity
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```json

{
  "id": "serve.need-entity.create",
  "ver": "1.0",
  "params": {
    "resmsgid": "",
    "msgid": "861533da-d815-4809-97c3",
    "err": "",
    "status": "SUCCESSFUL",
    "errmsg": ""
  },
  "responseCode": "OK",
  "result": {
    "needEntity": {
      "id": "1-d6844c76-b128-43cc-bbba"
    }
  }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
