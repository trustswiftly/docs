---
description: The API Key can be generated within your account settings.
---

# Users

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users" method="get" summary="Get Users" %}
{% swagger-description %}
List all the users currently assigned a profile.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-response status="200" description="Succesful response" %}
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
            "avatar": "https://cdn.trustswiftly.com/assets/img/profile.png",
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
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/api/users' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0'
```
{% endtab %}
{% endtabs %}

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users/{id}" method="get" summary="Get User" %}
{% swagger-description %}
Retrieve a specific users profile.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/api/users/2' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0'
```
{% endtab %}
{% endtabs %}

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users" method="post" summary="Create User" %}
{% swagger-description %}
Create a given users profile.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="notice" type="string" %}
Display a notice on the dashboard for users such as custom instructions.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Customer's email address.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="send_link" type="boolean" %}
Send a magic link to the user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="template_id" type="string" %}
ID of the verification template you wish to assign to this user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference_id" type="string" %}
An ID you can pass that correlates to your own system's user ID.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="integer" %}
Phone including international code. Example +13129450121
{% endswagger-parameter %}

{% swagger-parameter in="body" name="last_name" type="string" %}
Users last name.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="first_name" type="string" %}
Users first name.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="username" type="string" %}
A unique username for the given user.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
  "status": "success",
  "id": 69,
  "user_id": "3639",
  "magic_link": "https:\/\/test.trustswiftly.com\\/security-verify?expires=1325603631&key=16RWTtJRKTwjFIQCGWDEZrWkW4Qq2DdvfUQhdadug3AVwWu5mbZht&signature=768898ec51b20a623ba813969215f23785b784f213d04c0046265b3c6"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://{sub-domain}.trustswiftly.com/api/users' \
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

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users/{id}" method="patch" summary="Update User " %}
{% swagger-description %}
Update a provided user.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="username" type="string" %}
A unique username for the given user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="first_name" type="string" %}
Users first name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="last_name" type="string" %}
Users last name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="phone" type="integer" %}
Phone including international code.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference_id" type="string" %}
An ID you can pass that correlates to your own systems user ID.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="template_id" type="string" %}
ID of the verification template you wish to assign to this user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" type="string" %}
Customers email address.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request PATCH 'https://{sub-domain}.trustswiftly.com/api/users/1' \
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

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users/{id}/verifications" method="patch" summary="Update Verification" %}
{% swagger-description %}
Update a status of a verification
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="verification_id" type="string" %}
The ID corresponding to the verification name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="string" %}
The status to update the verification
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request PATCH 'https://{sub-domain}.trustswiftly.com/api/users/1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 2|GM2loELoTfc8rXC0PoC4WagW2eEQzE1AxhsqQ8Sn' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "verification_id": "7",
	"status": "2"
}
```
{% endtab %}
{% endtabs %}

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users/{id}" method="delete" summary="Delete User" %}
{% swagger-description %}
Delete a provided user.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to 
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request DELETE 'https://{sub-domain}.trustswiftly.com/api/users/1' \
--header 'Authorization: Bearer 1|GqRQaD0nMBmGkIKLiPuOPLAckxhupWyjVEZKjsj1' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw ''
```
{% endtab %}
{% endtabs %}

{% swagger baseUrl="https://{sub-domain}.trustswiftly.com" path="/api/users/{id}/verify-url" method="post" summary="Get Magic Link" %}
{% swagger-description %}
Generate a magic link used for user authentication
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
**API Key**

 is used for server-to-server communication to fetch sensitive data that you already have access to.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiration_hours" type="integer" %}
Hour(s) in which the magic link will remain alive before expiring.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "short_url": "https://tinyurl.com/y32d35rf",
    "full_url": "https://{sub-domain}.trustswiftly.com/security-verify?expires=1610753625&key=7&signature=3949637e17906a42bd3d0254af80a825f2696b9ba948cdf3654f0e354a2f6cef"
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://{sub-domain}.trustswiftly.com/api/users/1/verify-url' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer 1|GM2loELoTfc8rXC0PoC4WagW2eEQzE1AxhsqQ8Sn' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "expiration_hours": 24
}'
```
{% endtab %}
{% endtabs %}

