---
description: >-
  This sample call, which shows the Users API, includes a bearer token in the
  Authorization request header.
---

# Authentication

#### Specifying the user agent <a id="UserAgent"></a>

Each request to the API must be accompanied by a user agent request header. Typically this should be the name of the app consuming the service. A missing user agent will result in an HTTP 403 response. The user agent should accurately describe the nature of the API consumer such that it can be clearly identified in the request. Not doing so may result in the request being blocked. A valid request would look like:

#### Example Authenticated Request

{% tabs %}
{% tab title="Successful Request" %}
```text
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/account/api/users' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'User-Agent: TrustSwiftly/1.0' \ \
--header 'Authorization: Bearer {api_key}'
```
{% endtab %}

{% tab title="Authorization Error Response" %}
```
{
    "error_code": "000",
    "error_message": "Api Key Wrong or Unauthorized User"
}
```
{% endtab %}
{% endtabs %}



