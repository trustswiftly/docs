---
description: The API Key can be generated within your account settings.
---

# Users

## Get Users

<mark style="color:blue;">`GET`</mark> `https://{sub-domain}.trustswiftly.com/api/users`

List all the users currently assigned a profile.

#### Headers

| Name          | Type   | Description                                                                                                                                                               |
| ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization | string | <p><a href="authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p> |

{% tabs %}
{% tab title="200 Succesful response" %}
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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/api/users' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0'
```
{% endtab %}
{% endtabs %}

## Get User

<mark style="color:blue;">`GET`</mark> `https://{sub-domain}.trustswiftly.com/api/users/{id}`

Retrieve a specific users profile.

#### Headers

| Name          | Type   | Description                                                                                                                               |
| ------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization | string | <p><strong>API Key</strong></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p> |

{% tabs %}
{% tab title="200 " %}
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
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/api/users/2' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0'
```
{% endtab %}
{% endtabs %}

## Create User

<mark style="color:green;">`POST`</mark> `https://{sub-domain}.trustswiftly.com/api/users`

Create a given users profile.

#### Headers

<table><thead><tr><th>Name</th><th width="162">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td><p><a href="authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p></td></tr></tbody></table>

#### Request Body

<table><thead><tr><th>Name</th><th width="153">Type</th><th>Description</th></tr></thead><tbody><tr><td>notice</td><td>string</td><td>Display a notice on the dashboard for users such as custom instructions.</td></tr><tr><td>email</td><td>string</td><td>Customer's email address.</td></tr><tr><td>send_link</td><td>boolean</td><td>Send a magic link to the user via email.</td></tr><tr><td>template_id</td><td>string</td><td>ID of the verification template you wish to assign to this user.</td></tr><tr><td>reference_id</td><td>string</td><td>An ID you can pass that correlates to your own system's user ID.</td></tr><tr><td>phone</td><td>string</td><td>Phone including international code. Example +13129450121. It must be in <a href="https://www.twilio.com/docs/glossary/what-e164">E164 format.</a></td></tr><tr><td>last_name</td><td>string</td><td>Users last name.</td></tr><tr><td>first_name</td><td>string</td><td>Users first name.</td></tr><tr><td>username</td><td>string</td><td>A unique username for the given user.</td></tr><tr><td>send_sms</td><td>boolean</td><td>Send a magic link to the user via SMS.</td></tr><tr><td>custom_verify_data</td><td>json string</td><td>A json string listing any data validation requirements for a user during document verification. i.e. "custom_verify_data": {"last_name": "Smith"}</td></tr><tr><td>order_id</td><td>string</td><td>If the user is associated with a specific order or transaction.</td></tr><tr><td>completion_url</td><td>string</td><td>Optional custom URL unique per user to redirect to when verifications are completed. Otherwise in General Settings a URL can be set as default.</td></tr></tbody></table>

{% tabs %}
{% tab title="200 " %}
```javascript
{
  "status": "success",
  "id": 69,
  "magic_link": "https:\/\/test.trustswiftly.com\\/security-verify?expires=1325603631&key=16RWTtJRKTwjFIQCGWDEZrWkW4Qq2DdvfUQhdadug3AVwWu5mbZht&signature=768898ec51b20a623ba813969215f23785b784f213d04c0046265b3c6"
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://{sub-domain}.trustswiftly.com/api/users' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "email": "testing@test.com",
  "template_id": "tmpl_MQ"
}'
```
{% endtab %}
{% endtabs %}

## Update User&#x20;

<mark style="color:purple;">`PATCH`</mark> `https://{sub-domain}.trustswiftly.com/api/users/{id}`

Update a provided user.

#### Headers

| Name          | Type   | Description                                                                                                                                                               |
| ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization | string | <p><a href="authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p> |

#### Request Body

| Name                 | Type   | Description                                                                                      |
| -------------------- | ------ | ------------------------------------------------------------------------------------------------ |
| username             | string | A unique username for the given user.                                                            |
| first\_name          | string | Users first name                                                                                 |
| last\_name           | string | Users last name                                                                                  |
| phone                | string | Phone including international code.                                                              |
| reference\_id        | string | An ID you can pass that correlates to your own systems user ID.                                  |
| template\_id         | string | ID of the verification template you wish to assign to this user.                                 |
| email                | string | Customers email address.                                                                         |
| custom\_verify\_data | String | A json string listing any data validation requirements for a user during document verification.  |
| order\_id            | string | If the user is associated with a specific order or transaction.                                  |

{% tabs %}
{% tab title="200 " %}
```
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request PATCH 'https://{sub-domain}.trustswiftly.com/api/users/1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
    "first_name": "New",
    "last_name": "Name",
    "template_id": "tmpl_MQ"
}'
```
{% endtab %}
{% endtabs %}

## Update Verification

<mark style="color:purple;">`PATCH`</mark> `https://{sub-domain}.trustswiftly.com/api/users/{id}/verifications`

Update a status of a verification

#### Headers

| Name          | Type   | Description                                                                                                                                                               |
| ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Authorization | string | <p><a href="authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p> |

#### Request Body

| Name             | Type   | Description                                   |
| ---------------- | ------ | --------------------------------------------- |
| verification\_id | string | The ID corresponding to the verification name |
| status           | string | The status to update the verification         |

{% tabs %}
{% tab title="200 " %}
```
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request PATCH 'https://{sub-domain}.trustswiftly.com/api/users/1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "verification_id": "7",
	"status": "2"
}
```
{% endtab %}
{% endtabs %}

## Delete User

<mark style="color:red;">`DELETE`</mark> `https://{sub-domain}.trustswiftly.com/api/users/{id}`

Delete a provided user.

#### Headers

| Name          | Type   | Description                                                                                                                                                              |
| ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Authorization | string | <p><a href="authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to</p> |

{% tabs %}
{% tab title="200 " %}
```
{
    "success": true
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request DELETE 'https://{sub-domain}.trustswiftly.com/api/users/1' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw ''
```
{% endtab %}
{% endtabs %}

## Get Magic Link

<mark style="color:green;">`POST`</mark> `https://{sub-domain}.trustswiftly.com/api/users/{id}/verify-url`

Generate a magic link used for user authentication

#### Headers

| Name          | Type   | Description                                                                                                                                                                                            |
| ------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Authorization | string | <p><a href="authentication.md#authorization-error-response"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p> |

#### Request Body

| Name              | Type    | Description                                                        |
| ----------------- | ------- | ------------------------------------------------------------------ |
| expiration\_hours | integer | Hour(s) in which the magic link will remain alive before expiring. |

{% tabs %}
{% tab title="200 " %}
```
{
    "short_url": "https://tinyurl.com/y32d35rf",
    "full_url": "https://{sub-domain}.trustswiftly.com/security-verify?expires=1610753625&key=7&signature=3949637e17906a42bd3d0254af80a825f2696b9ba948cdf3654f0e354a2f6cef"
}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --location --request POST 'https://{sub-domain}.trustswiftly.com/api/users/1/verify-url' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}' \
--header 'User-Agent: TrustSwiftly/1.0' \
--data-raw '{
  "expiration_hours": 24
}'
```
{% endtab %}
{% endtabs %}
