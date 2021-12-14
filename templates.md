---
description: Get available verification templates
---

# Templates

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com/account" path="/api/settings/templates/verifications" method="get" summary="Get Verifications Templates" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
[
  {
    "id": 1,
    "name": "tmpl_MQ",
    "types": [
      "Email"
    ]
  },
  {
    "id": 2,
    "name": "tmpl_Mg",
    "types": [
      "Phone \/ SMS",
      "Document \/ ID"
    ]
  },
  {
    "id": 3,
    "name": "tmpl_Mw",
    "types": [
      "Phone \/ SMS",
      "Document \/ ID"
    ]
  }
]
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/account/api/settings/templates/verifications' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}'
```
{% endtab %}
{% endtabs %}
