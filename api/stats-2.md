---
description: Get current stats for verifications.
---

# Stats

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/stats" method="get" summary="Get Verification Stats" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "users_per_month": {
    "January": 0,
    "February": 0,
    "March": 1,
    "April": 0,
    "May": 0,
    "June": 0,
    "July": 0,
    "August": 2,
    "September": 0,
    "October": 0,
    "November": 0,
    "December": 0
  },
  "users_per_status": {
    "total": 3,
    "new": 2,
    "banned": 0,
    "unconfirmed": 1
  },
  "latest_registrations": [
    {
      "id": 123,
      "first_name": "John",
      "last_name": "Doe",
      "username": "johndoe",
      "email": "john.doe@gmail.com",
      "phone": "+381641234567",
      "avatar": "http://yourwebsite.com/users/milos-avatar.jpg",
      "address": "Some random street, 123, Serbia",
      "country_id": 688,
      "role_id": 1,
      "status": "Active",
      "birthday": "1989-01-03",
      "last_login": "2017-04-27 16:47:59",
      "two_factor_country_code": 381,
      "two_factor_phone": "6412345678",
      "two_factor_options": {
        "option1": 4,
        "option2": "option value"
      },
      "created_at": "2017-04-20 16:47:59",
      "updated_at": "2017-04-27 10:47:59"
    },
    "..."
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/api/stats' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}'
```
{% endtab %}
{% endtabs %}
