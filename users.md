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
**Bearer token** is used for server-to-server communication to fetch sensitive data that you already have access to.
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
            "last_name": "Test",
            "username": "trusttest",
            "email": "test@trustswiftly.dev",
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
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**Bearer token** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}
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
        "last_name": "Test",
        "username": "trusttest",
        "email": "test@trustswiftly.dev",
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

{% api-method method="post" host="https://{sub-domain}.trustswiftly.com/account" path="/api/users" %}
{% api-method-summary %}
Create User
{% endapi-method-summary %}

{% api-method-description %}
Create a given users profile.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**Bearer token** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
Customer's email address.
{% endapi-method-parameter %}

{% api-method-parameter name="send\_link" type="boolean" required=false %}
Send a magic link to the user.
{% endapi-method-parameter %}

{% api-method-parameter name="templateId" type="integer" required=false %}
ID of the verification template you wish to assign to this user.
{% endapi-method-parameter %}

{% api-method-parameter name="reference\_id" type="string" required=false %}
An ID you can pass that correlates to your own system's user/account ID.
{% endapi-method-parameter %}

{% api-method-parameter name="phone" type="integer" required=false %}
Phone including international code.
{% endapi-method-parameter %}

{% api-method-parameter name="last\_name" type="string" required=false %}
Users last name.
{% endapi-method-parameter %}

{% api-method-parameter name="first\_name" type="string" required=false %}
Users first name.
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=false %}
A unique username for the given users email.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "id": 7,
    "token": "MnxMeUwxUUxUWXFQTFdObVhPTm1FYnFlU1cxZ2IwOElzcE9qUmdUN1Ra"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://{sub-domain}.trustswiftly.com/account" path="/api/users/{id}" %}
{% api-method-summary %}
Delete User
{% endapi-method-summary %}

{% api-method-description %}
Delete a provided user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**Bearer token** is used for server-to-server communication to fetch sensitive data that you already have access to 
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

