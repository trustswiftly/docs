---
description: The API Key can be generated within your account settings.
---

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
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Succesful response
{% endapi-method-response-example-description %}

```
{
    "data": [
        {
            "id": 5,
            "first_name": "AutoTest",
            "last_name": "User",
            "username": "codecept_user",
            "email": "codecept_user@trustswiftly.dev",
            "verifications": [
                {
                    "id": 1,
                    "name": "Email",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 2,
                    "name": "Phone / SMS",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 3,
                    "name": "Document / ID",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 4,
                    "name": "PayPal",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 5,
                    "name": "Video",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 6,
                    "name": "Voice",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 7,
                    "name": "Secure Card",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 8,
                    "name": "Geolocation",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 9,
                    "name": "Social Account",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                },
                {
                    "id": 10,
                    "name": "Two-Step Authentication",
                    "status": {
                        "value": 0,
                        "friendly": "Pending"
                    }
                }
            ],
            "phone": null,
            "avatar": "https://cdn.trustswiftly.com/account/assets/img/profile.png",
            "address": null,
            "country_id": null,
            "role_id": 2,
            "status": "Active",
            "birthday": null,
            "last_login": "2020-09-07 19:56:35",
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

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/account/api/users' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0'
```
{% endtab %}
{% endtabs %}

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
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to.
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
        "id": 7,
        "first_name": "New",
        "last_name": "Name",
        "username": "Verify_User2101131027492493",
        "email": "testing@test.com",
        "verifications": [
            {
                "id": 1,
                "name": "Email",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 2,
                "name": "Phone / SMS",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 3,
                "name": "Document / ID",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 4,
                "name": "PayPal",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 5,
                "name": "Video",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 6,
                "name": "Voice",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 7,
                "name": "Secure Card",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 8,
                "name": "Geolocation",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 9,
                "name": "Social Account",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 10,
                "name": "Two-Step Authentication",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 11,
                "name": "Bank",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            },
            {
                "id": 12,
                "name": "Live Video",
                "status": {
                    "value": 0,
                    "friendly": "Pending"
                }
            }
        ],
        "phone": null,
        "avatar": "https://images.trustswiftly.com/public/avatars/none.png",
        "address": null,
        "country_id": null,
        "role_id": 2,
        "status": "Active",
        "birthday": null,
        "last_login": "2021-01-14 03:33:33",
        "two_factor_country_code": 0,
        "two_factor_phone": "",
        "two_factor_options": null,
        "email_verified_at": null,
        "created_at": "2021-01-13 22:27:49",
        "updated_at": "2021-01-14 03:33:33"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/account/api/users/2' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0'
```
{% endtab %}
{% endtabs %}

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
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="notice" type="string" required=false %}
Display a notice on the dashboard for users such as custom instructions.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
Customer's email address.
{% endapi-method-parameter %}

{% api-method-parameter name="send\_link" type="boolean" required=false %}
Send a magic link to the user.
{% endapi-method-parameter %}

{% api-method-parameter name="template\_id" type="string" required=true %}
ID of the verification template you wish to assign to this user.
{% endapi-method-parameter %}

{% api-method-parameter name="reference\_id" type="string" required=false %}
An ID you can pass that correlates to your own system's user/account ID.
{% endapi-method-parameter %}

{% api-method-parameter name="phone" type="integer" required=false %}
Phone including international code. Example +13129450121
{% endapi-method-parameter %}

{% api-method-parameter name="last\_name" type="string" required=false %}
Users last name.
{% endapi-method-parameter %}

{% api-method-parameter name="first\_name" type="string" required=false %}
Users first name.
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=false %}
A unique username for the given user.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "status": "success",
    "id": 7,
    "token": "MnxMeUwxUUxUWXFQTFdObVhPTm1FYnFlU1cxZ2IwOElzcE9qUmdUN1Ra"
    "magic_link": "https:\/\/www.trustswiftly.com\/account\/security-verify?email=1&expires=1616798987&key=13srgDmUj4hjySJAaaCi2d1hPx3ETvQHFDBfAgD1o5BsEaCsdzFc&signature=330beea028779412193ada9217f14b77e6a168c3d634afbf222418e1e5022f34"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://{sub-domain}.trustswiftly.com/account/api/users' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "email": "testing@test.com",
  "template_id": "tmpl_MQ"
}'
```
{% endtab %}
{% endtabs %}

{% api-method method="patch" host="https://{sub-domain}.trustswiftly.com/account" path="/api/users/{id}" %}
{% api-method-summary %}
Update User 
{% endapi-method-summary %}

{% api-method-description %}
Update a provided user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="username" type="string" required=false %}
A unique username for the given user.
{% endapi-method-parameter %}

{% api-method-parameter name="first\_name" type="string" required=false %}
Users first name
{% endapi-method-parameter %}

{% api-method-parameter name="last\_name" type="string" required=false %}
Users last name
{% endapi-method-parameter %}

{% api-method-parameter name="phone" type="integer" required=false %}
Phone including international code.
{% endapi-method-parameter %}

{% api-method-parameter name="reference\_id" type="string" required=false %}
An ID you can pass that correlates to your own systems user/account ID.
{% endapi-method-parameter %}

{% api-method-parameter name="template\_id" type="string" required=true %}
ID of the verification template you wish to assign to this user.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=false %}
Customers email address.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
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

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request PATCH 'https://{sub-domain}.trustswiftly.com/account/api/users/1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 2|GM2loELoTfc8rXC0PoC4WagW2eEQzE1AxhsqQ8Sn' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
    "first_name": "New",
    "last_name": "Name",
    "template_id": "tmpl_MQ"
}'
```
{% endtab %}
{% endtabs %}

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
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to 
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

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request DELETE 'https://{sub-domain}.trustswiftly.com/account/api/users/1' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw ''
```
{% endtab %}
{% endtabs %}

{% api-method method="post" host="https://{sub-domain}.trustswiftly.com/account" path="/api/users/{id}/verify-url" %}
{% api-method-summary %}
Get Magic Link
{% endapi-method-summary %}

{% api-method-description %}
Generate a magic link used for user authentication
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
**API Key** is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="expiration\_hours" type="integer" required=false %}
Hour\(s\) in which the magic link will remain alive before expiring.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "short_url": "https://tinyurl.com/y32d35rf",
    "full_url": "https://{sub-domain}.trustswiftly.com/account/security-verify?expires=1610753625&key=7&signature=3949637e17906a42bd3d0254af80a825f2696b9ba948cdf3654f0e354a2f6cef"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://{sub-domain}.trustswiftly.com/account/api/users/1/verify-url' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GM2loELoTfc8rXC0PoC4WagW2eEQzE1AxhsqQ8Sn' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "expiration_hours": 24
}'
```
{% endtab %}
{% endtabs %}



