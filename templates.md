---
description: Get available verification templates
---

# Templates

## List Verification Templates

Verification Templates define the specific sequence of checks a user must complete (e.g., "Email only", or "ID Document + Selfie Scan").

You can use this endpoint to programmatically fetch a list of all available templates configured in your account. This is essential for dynamically assigning the correct verification flow to a user when you create or update them via the API.

<mark style="color:blue;">`GET`</mark>` ``https://{sub-domain}.trustswiftly.com/api/settings/templates/verifications`

***

#### Authentication

Authentication is handled via the `Authorization` header. There are no path or query parameters for this endpoint.

<table><thead><tr><th width="162">Header</th><th width="115.66668701171875">Type</th><th width="124">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>Authorization</code></td><td>string</td><td>Yes</td><td>Your secret API key, prefixed with <code>Bearer</code> .</td></tr><tr><td><code>Accept</code></td><td>string</td><td>Yes</td><td>Must be <code>application/json</code>.</td></tr></tbody></table>

***

#### Understanding the Response Body

The endpoint returns an array of your configured Verification Template objects. Each object contains the template's ID and the types of checks it includes.

<table><thead><tr><th width="159">Field</th><th width="109.3333740234375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>id</code></td><td>number</td><td>The internal numeric identifier for the template.</td></tr><tr><td><code>name</code></td><td>string</td><td>The <strong>Template ID</strong> (e.g., <code>tmpl_MQ</code>). <strong>This is the value you must use in the <code>template_id</code> field when creating or updating users.</strong></td></tr><tr><td><code>types</code></td><td>array</td><td>A list of the verification methods included in this template (e.g., "Email", "Document / ID").</td></tr></tbody></table>

***

#### Example Request & Response

**Request**

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/settings/templates/verifications' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

**Response**

The response will be an array of all templates available in your account.

```json
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
      "Phone / SMS",
      "Document / ID"
    ]
  },
  {
    "id": 3,
    "name": "tmpl_Mw",
    "types": [
      "Phone / SMS",
      "Document / ID",
      "Selfie"
    ]
  }
]
```

***

#### What's Next: Using a Template ID

After you've fetched your templates, you can use the value from the `name` field to assign a verification flow to a user.

For example, if you want to assign the second template from the response above (`tmpl_Mg`) to a new user, your API call to create the user would look like this:

```bash
# Example of using a template_id when creating a user

curl --request POST \
  --url https://app.trustswiftly.com/api/users \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "reference_id": "user_12345",
    "email": "test@example.com",
    "template_id": "tmpl_Mg"  // <-- The ID from the templates endpoint
  }'
```

For more details, see the Create User API documentation.
