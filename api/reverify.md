---
description: >-
  Use the reverify API to automatically verify the facial attributes of a user
  on subsequent verifications.
---

# Reverify User

## Re-verify User Identity

This endpoint is designed for "step-up" authentication or low-friction re-verification. It allows you to dynamically switch a user from their initial, comprehensive verification process to a simpler one for subsequent checks.

The primary use case is to switch a user from an initial, high-assurance **Verification Template** (e.g., `ID Document + Selfie Scan`) to a subsequent, low-friction template (e.g., `Selfie Scan Only`).

This is ideal for scenarios where you need to re-confirm a user's identity without making them repeat the entire onboarding process.

**Common Use Cases**

* **Periodic Identity Check:** A user registered a month ago with their ID and a selfie. To access a high-value area of your service, you require them to quickly re-verify their identity with just a new selfie.
* **Password Reset:** Before allowing a password reset, you can require the user to pass a quick selfie check to ensure the legitimate owner is making the request.

> **Note:** This API is specifically for switching between verification templates, most commonly for facial re-verification. For other authentication methods like Passkeys or OTP, you should use the standard Update User endpoint to assign a different template.

***

### Reverify Endpoint

This endpoint assigns a new, temporary verification template to a user. All requests should be made to your account's specific sub-domain.

<mark style="color:green;">`POST`</mark> `https://{sub-domain}.trustswiftly.com/api/user/document/reverify`

**Request Body**

<table><thead><tr><th width="225.66668701171875">Parameter</th><th width="103.33331298828125">Type</th><th width="81.6666259765625">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>user_id</code></td><td>string</td><td>Yes</td><td>The <strong>Trust Swiftly User ID</strong> (e.g., <code>647</code>). <strong>Note:</strong> This is the internal <code>id</code> returned by the Trust Swiftly API when you created the user, not your own <code>reference_id</code>.</td></tr><tr><td><code>current_workflow_id</code></td><td>string</td><td>Yes</td><td>The ID of the <strong>Verification Template</strong> (workflow) that the user originally verified with. See below for how to find this ID.</td></tr><tr><td><code>re_verify_workflow_id</code></td><td>string</td><td>Yes</td><td>The ID of the new, simpler <strong>Verification Template</strong> you want to assign for this specific re-verification check.</td></tr></tbody></table>

**How to Find Workflow IDs**

Your "Verification Templates" are referred to as workflows in this API call. You can find the necessary `workflow_id` values in your Trust Swiftly dashboard.

1. Navigate to **Settings > Documents > User Verify WorkFlow**.
2. You will see a list of all your configured wrokflows. The ID (e.g., `flow_MzA`) for each is displayed next to its name.

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption><p>Copy Workflow ID</p></figcaption></figure>

***

#### Example Request

In this example, we are switching user `647` from an "ID Document & Selfie" template (`flow_MzA`) to a new "Selfie Only" template (`flow_Mjk`).

```bash
curl --request POST \
  --url https://{sub-domain}.trustswiftly.com/api/user/document/reverify \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "user_id": "647",
    "current_workflow_id": "flow_MzA",
    "re_verify_workflow_id": "flow_Mjk"
  }'
```

***

#### Responses

**Success (200 OK)**

A successful request will return a `200 OK` status code. The user has now been assigned the new template. The next time they access their `magic_link`, they will be prompted with the re-verification flow.

```json
{
  "success": true
}
```

**Error Responses**

Your application should be prepared to handle the following errors.

*   **User Already Assigned to Target Workflow**

    * This error occurs if the user is already assigned to the template specified in `re_verify_workflow_id`. This can happen if you make the same API call twice. The first call succeeds, and the second fails with this error.

    ```json
    {
      "Error_type": "already_assigned",
      "error_message": "Already assigned"
    }
    ```
*   **User Not Found (`404 Not Found`)**

    * Returned if the `user_id` does not exist.

    ```json
    { "message": "User not found." }
    ```
*   **Invalid Data (`422 Unprocessable Entity`)**

    * Returned if the `current_workflow_id` does not match the user's current template.

    ```json
    {
      "message": "The given data was invalid.",
      "errors": {
        "current_workflow_id": ["The selected current workflow id is invalid or does not match the user's workflow."]
      }
    }
    ```
