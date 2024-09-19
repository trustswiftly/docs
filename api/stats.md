---
description: >-
  Use the reverify API to automatically verify the facial attributes of a user
  on subsequent verifications.
---

# Reverify User

The reverification endpoint is useful for customers looking to streamline their identity verification process. There are multiple methods for reverifications and Trust Swiftly supports each one depending on the level of assurance required.&#x20;

Example use cases:

1. User enrolls / registers themselves with their base verification case. i.e. Identity Document + Selfie
2. User revisits service in the future and is required to reverify themselves with only a selfie. Instead of asking them for multiple checks a quicker verification can be completed with just their face.&#x20;

Other reverification use cases can be through a Passkey (Phone Authenticator) or OTP Authenticator. Using this method the API for reverify is not needed as the reverify API is only for Facial reverifications, instead the normal Users API can be used to update the verification template.

1. User enrolls / registers themselves with their base verification template.&#x20;
2. User revisits service for another verification and only is required to authenticate through Face ID / Fingerprint or other bound device-based authenticator.&#x20;

## Reverify Document

<mark style="color:green;">`POST`</mark> `https://{sub-domain}.trustswiftly.com/api/document/reverify`

Get the workflow ID of the current and new documents in the Trust Swiftly dashboard for document settings.

#### Headers

<table><thead><tr><th width="174">Name</th><th width="81">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td><p><a href="../authentication.md"><strong>API Key</strong></a></p><p>is used for server-to-server communication to fetch sensitive data that you already have access to.</p></td></tr></tbody></table>

#### Request Body

<table><thead><tr><th width="230">Name</th><th width="92">Type</th><th>Description</th></tr></thead><tbody><tr><td>current_workflow_id</td><td>string</td><td>Display a notice on the dashboard for users such as custom instructions.</td></tr><tr><td>re_verify_workflow_id</td><td>string</td><td>Customer's email address.</td></tr><tr><td>user_id</td><td>string</td><td>Send a magic link to the user via email.</td></tr></tbody></table>

{% tabs %}
{% tab title="200 " %}
```json
{
	"success": true
}
```
{% endtab %}

{% tab title="Error" %}
{

"Error\_type":"already\_assigned",

"error\_message":"Already assigned"

}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="cURL" %}
```bash
curl --request POST \
  --url https://{sub-domain}.trustswiftly.com/api/user/document/reverify \
  --header 'Authorization: Bearer {api_key}' \
  --header 'Content-Type: application/json' \
  --header 'User-Agent: insomnium/1.0' \
  --data '{
  "current_workflow_id": "flow_MzA",
  "re_verify_workflow_id": "flow_Mjk",
  "user_id": "647"
}'
```
{% endtab %}
{% endtabs %}
