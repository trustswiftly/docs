---
description: Get available verification templates
---

# Templates

{% api-method method="get" host="https://{sub-domain}.trustswiftly.com/account" path="/api/settings/templates/verifications" %}
{% api-method-summary %}
Get Verifications Templates
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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

