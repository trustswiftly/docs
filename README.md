---
description: >-
  This documentation will show you how to integrate Trust Swiftly into your Web
  Application and communicate with our private API.
---

# Developer Documentation

### Quickstart Overview

| Integration Options (Web)                                                                                                         | Details                                                                                                                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><a href="getting-an-api-key.md">Rest API</a></p><p> (Average 3-7 day effort to setup)</p>                                      | Use the API to programmatically add users and modify required verifications. The API can be used by using the magic link to create a simple verification button. You are not able to directly send us images to analyze for documents. All verifications must be completed through the hosted link for security. |
| [No Code Managed](hosted/share-hosted-link.md)                                                                                    | Use the no code integration to share a simple link through email, chat, or SMS which will redirect the user to a hosted page to complete verifications. This method requires an admin to add the user to verify manually and then review them once complete.                                                     |
| [iOS and Android Apps](web/webview-ios-and-android.md)                                                                            | Use iOS and Android webview implementations to integrate your native app with Trust Swiftly.                                                                                                                                                                                                                     |
| <p><a href="self-sign-up-and-create-autofill/configure-self-verifications.md">No Code Self-Signup</a> </p><p>(3-minute setup)</p> | Direct users to our signup page to register details themselves for onboarding and then allow them to complete the template verification request. This method requires no upfront work and can be used as customer identity management platform.                                                                  |

Each method to integrate above has pros and cons depending on your use case. For the simplest and fastest to manage process the no code self-signup works well. For more custom options we recommend our API.

***

#### Quickstart Guide

Welcome to Trust Swiftly! This guide will walk you through the essential end-to-end workflow in under 5 minutes. By the end, you will have created a user, retrieved their unique verification link, and received a webhook confirming their completion.

Let's get started.

**Prerequisites**

Before you begin, you'll need two things from your Trust Swiftly Dashboard:

1. **Your API Key:** Found under **Settings > API**.
2. **Your Webhook Signing Secret:** Found under **Settings > Webhooks**.

Keep these handy for the next steps.

***

#### Step 1: Create a User via the API

First, we'll register a new user in the Trust Swiftly system. The `reference_id` is crucial; this is your internal ID for the user (e.g., their ID from your database).

Open your terminal and run the following `curl` command. Make sure to replace `YOUR_API_KEY` with your actual key.

```bash
curl -X POST https://company.trustswiftly.com/api/users \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "reference_id": "user_12345",
    "email": "test@example.com",
    "first_name": "John",
    "last_name": "Doe"
  }'
```

You will receive a successful response containing the new user's details, including their unique Trust Swiftly `id` and a `magic_link`.

**✅ Successful Response:**

```json
{
	"status": "success",
	"id": 93,
	"magic_link": "https://company.trustswiftly.dev/security-verify?email=0&expires=1745613424&key=1ACSv57lwn7Z8Y0hF9V3&signature=cd6423294e2328a4fc85e7bc0410d3a&code=FC721Np"
}
```

**Tip:** The `magic_link` is the unique URL you will provide to your user to start their verification process.

***

#### Step 2: Set Up a Webhook Endpoint

To get notified when a user completes their verification, you need to set up a webhook endpoint. For this guide, we'll use the free service [webhook.site](https://webhook.site/) to create a temporary URL to inspect the payloads.

1. Open [webhook.site](https://webhook.site/) in a new tab. It will automatically generate a unique URL for you. Copy it.
2. In your Trust Swiftly Dashboard, navigate to **Settings > Webhooks**.
3. Paste the webhook.site URL into the **Endpoint URL** field and save your changes.

This will now send all events from your account to your temporary `webhook.site` page.

***

#### Step 3: Trigger a Verification Event

Now, let's trigger a test event.

1. Take the `magic_link` you received in the Step 1 response.
2. Open it in your web browser. (Use incognito or separate browser to maintain your Admin portal)
3. You will see the Trust Swiftly verification flow. Complete the steps.

***

#### Step 4: Confirm the Webhook

Once you complete the verification, Trust Swiftly will send a `verification.completed` event to the URL you configured.

Go back to your `webhook.site` page. You will see a new POST request appear on the left. Click on it to inspect the payload. It will be a JSON object that looks like this:

**✅ Webhook Payload Received:**

```json
{
  "id": "evt_fedcba98765",
  "event": "verification.completed",
  "created_at": "2024-10-26T12:05:00Z",
  "reference_id": "user_12345",
  "verifications": [
    {
      "name": "Email",
      "status": { "friendly": "done", "code": 100 }
    }
  ]
}
```

Notice that the `reference_id` matches the one you sent in Step 1. This is how you associate the verification event back to a user in your system.

***

#### What's Next?

Congratulations! You've successfully completed the core Trust Swiftly integration workflow.

Here's where to go from here:

* **Secure Your Endpoint:** Learn how to use your Signing Secret to verify that webhooks are genuinely from Trust Swiftly.
  * [**Verifying Webhook Signatures**](webhooks/code-examples.md)
* **Build a Robust Handler:** See our best practices for processing webhooks reliably.
  * [**Handling Webhooks**](webhooks/code-examples.md)
* **Explore the API:** Dive into the full API Reference to see what else you can do.
  * [**API Reference**](users.md)
