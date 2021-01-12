# Users

{% api-method method="get" host="https://{sub-domain}.trustswiftly.com/account" path="/api/users" %}
{% api-method-summary %}
Get Users
{% endapi-method-summary %}

{% api-method-description %}
List all the users currently assigned a profile.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**Bearer token** is used for server-to-server communication, is used to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "data": [
        {
            "id": 1,
            "first_name": "Trust",
            "last_name": "Admin",
            "username": "trustadmin",
            "email": "admin@trustswiftly.dev",
            "phone": "+12524653705",
            "avatar": "https://cdn.trustswiftly.com/account/assets/img/profile.png",
            "address": null,
            "country_id": null,
            "role_id": 1,
            "status": "Active",
            "birthday": null,
            "last_login": "2020-09-11 20:07:38",
            "two_factor_country_code": 0,
            "two_factor_phone": "",
            "two_factor_options": null,
            "email_verified_at": null,
            "created_at": "2020-09-11 01:33:51",
            "updated_at": "2020-09-11 01:33:51"
        }
    ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://{sub-domain}.trustswiftly.com/account" path="/api/users/{id}" %}
{% api-method-summary %}
Get User
{% endapi-method-summary %}

{% api-method-description %}
Retrieve a specific users profile.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**Bearer token** is used for server-to-server communication, is used to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "data": {
        "id": 1,
        "first_name": "Trust",
        "last_name": "Admin",
        "username": "trustadmin",
        "email": "admin@trustswiftly.dev",
        "phone": "+12524653705",
        "avatar": "https://cdn.trustswiftly.com/account/assets/img/profile.png",
        "address": null,
        "country_id": null,
        "role_id": 1,
        "status": "Active",
        "birthday": null,
        "last_login": "2020-09-11 20:07:38",
        "two_factor_country_code": 0,
        "two_factor_phone": "",
        "two_factor_options": null,
        "email_verified_at": null,
        "created_at": "2020-09-11 01:33:51",
        "updated_at": "2020-09-11 01:33:51"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

