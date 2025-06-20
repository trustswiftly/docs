---
description: >-
  Learn how to manually generate and share a unique verification link for a
  single user directly from the Trust Swiftly dashboard. This simple, no-code
  method is ideal for one-off verifications or proof
---

# Share hosted link

## Sharing a Manual Verification Link

This guide covers the simplest, no-code method for verifying a single user by sharing a unique link directly from your Trust Swiftly dashboard.

This method is ideal for:

* Quickly verifying a specific individual.
* Getting started without writing any code.
* Proof-of-concept testing.

When you need to automate this process for many users, we recommend using the Trust Swiftly API to create users and retrieve their links programmatically.

***

#### How it Works

The process involves two main stages: first creating a user in the dashboard, and then generating and sharing their unique verification link.

**Step 1: Create the User**

Before you can get a verification link, a user must exist in the Trust Swiftly system.

1. From your Trust Swiftly dashboard, navigate to the **Users** page.
2. Click the **Add User** button.
3. Fill in the user's details and click **Save**.

**Step 2: Generate and Share the Verification Link**

Once the user has been created, they will appear in the user list.

1. Find the user in the list on the **Users** page.
2. Click the **Share Verify URL** button.

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

**Step 3: Choose Your Sharing Method**

A dialog box will appear with several options for sharing the link.

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

* **Copy Link:** Click the copy icon to copy the full verification URL to your clipboard. You can then paste this link into an email, SMS, live chat, or use it to generate a QR code.
* **Send Email:** Enter the user's email address and click **Send Email** to have Trust Swiftly send a notification directly to the user with their link.
* **Send SMS:** If the phone is provided during user creation a SMS can be sent to their phone with a link to start the verification.&#x20;
* **Modify Expiration:** By default, the link has a set expiration time for security. You can adjust this duration here if needed.

> **Important: This Link is a One-Time Secret**> \
> The verification link is sensitive and provides direct access to a user's verification session.
>
> * **Share it only with the intended user.**
> * **Do not post it in a public place.**
> * Once a user starts or completes the verification, the link cannot be reused.

***

#### The User's Experience

When your user clicks the link, they will be taken to your branded, hosted verification page where they can complete the required steps (e.g., uploading an ID, taking a selfie).

Once they are finished, their status will be updated in your Trust Swiftly dashboard, and a webhook will be sent to your endpoint if you have one configured.
