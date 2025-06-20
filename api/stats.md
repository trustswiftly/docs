---
description: Get current stats for verifications.
---

# Stats

## Get Account Statistics

This endpoint provides a high-level snapshot of your account's verification activity, including user registration volume, a breakdown of user statuses, and a list of the most recent user records.

This is useful for building dashboards or for periodic reporting on your verification funnel.

<mark style="color:blue;">`GET`</mark>` ``https://{sub-domain}.trustswiftly.com/api/stats`

***

#### Authentication

Authentication is handled via the `Authorization` header. There are no path or query parameters for this endpoint.

<table><thead><tr><th width="174">Header</th><th width="128.3333740234375">Type</th><th width="83">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>Authorization</code></td><td>string</td><td>Yes</td><td>Your secret API key, prefixed with <code>Bearer</code> .</td></tr><tr><td><code>Accept</code></td><td>string</td><td>Yes</td><td>Must be <code>application/json</code>.</td></tr></tbody></table>

***

#### Understanding the Response Body

The response object is composed of three main sections:

**`users_per_month`**

This object provides a monthly breakdown of total user registrations for the current calendar year.

```json
"users_per_month": {
    "January": 0,
    "February": 0,
    "March": 1,
    // ...etc
}
```

**`users_per_status`**

This object gives you a real-time count of users categorized by their current status within the Trust Swiftly system.

<table><thead><tr><th width="138.6666259765625">Status</th><th>Description</th></tr></thead><tbody><tr><td><code>total</code></td><td>The total number of user records associated with your account.</td></tr><tr><td><code>new</code></td><td>Users who have been created but have not yet started a verification flow.</td></tr><tr><td><code>banned</code></td><td>Users who have been explicitly banned.</td></tr><tr><td><code>unconfirmed</code></td><td>Users who are in a pending or processing state.</td></tr></tbody></table>

```json
"users_per_status": {
    "total": 3,
    "new": 2,
    "banned": 0,
    "unconfirmed": 1
}
```

**`latest_registrations`**

This is an array containing the full user objects for the most recently created users on your account. While the full object is returned, the most relevant fields for statistical purposes are typically:

<table><thead><tr><th width="190">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>id</code></td><td>The user's unique ID within the Trust Swiftly system.</td></tr><tr><td><code>first_name</code></td><td>The user's first name.</td></tr><tr><td><code>last_name</code></td><td>The user's last name.</td></tr><tr><td><code>email</code></td><td>The user's email address.</td></tr><tr><td><code>status</code></td><td>The current status of the user (e.g., "Active", "Unconfirmed").</td></tr><tr><td><code>created_at</code></td><td>The timestamp when the user was created.</td></tr></tbody></table>

***

#### Example Request & Full Response

**Request**

```bash
curl --request GET \
  --url https://{sub-domain}.trustswiftly.com/api/stats \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

**Full Response**

<details>

<summary><strong>Click to expand the full example response</strong></summary>

```json
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
    {
      "id": 124,
      "first_name": "Jane",
      "last_name": "Smith",
      "username": "janesmith",
      "email": "jane.smith@gmail.com",
      "phone": "+1234567890",
      "avatar": null,
      "address": "123 Main St, Anytown, USA",
      "country_id": 840,
      "role_id": 1,
      "status": "Unconfirmed",
      "birthday": "1992-05-15",
      "last_login": null,
      "two_factor_country_code": null,
      "two_factor_phone": null,
      "two_factor_options": {},
      "created_at": "2024-09-20 11:30:00",
      "updated_at": "2024-09-20 11:30:00"
    }
  ]
}
```

</details>
