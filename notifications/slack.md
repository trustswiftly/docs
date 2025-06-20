---
description: Setup Slack notifications to be alerted about new verification statuses.
---

# Slack

**Configuring Slack Notifications**

Stay informed about key verification events in real-time by integrating Trust Swiftly with your Slack workspace. This setup allows you to receive instant notifications, enabling your team to monitor statuses and respond quickly to verifications that require manual review.

**Step 1: Create an Incoming Webhook in Slack**

First, you need to generate a unique webhook URL from your Slack account. This URL will be used by Trust Swiftly to send notifications directly to a channel of your choice.

1. **Create or Choose a Slack Channel:** Decide which channel you want to receive notifications in. It's often best to create a new, dedicated channel, such as `#verification-alerts` or `#trust-swiftly-logs`, to keep these updates organized.
2. **Generate the Webhook URL:**
   * Navigate to the Slack API documentation for Incoming Webhooks: [https://api.slack.com/messaging/webhooks](https://api.slack.com/messaging/webhooks)
   * Follow the on-screen instructions to create a new webhook. You will be prompted to select the channel you prepared in the previous step.
   * Once created, Slack will generate a unique Webhook URL. It will look something like this:     `https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX`
   * Click **Copy** to save this URL for the next step.

**Step 2: Configure Notification Events in Trust Swiftly**

Next, add the webhook URL to your Trust Swiftly settings and select which events you want to be notified about.

1. **Navigate to Notification Settings:** In your Trust Swiftly dashboard, go to **Settings** -> **Notifications** and select the **Slack** tab.
2. **Add Webhook URL:** Paste the Slack webhook URL you copied into the **Webhook URL** field.
3. **Subscribe to Events:** Below the URL field, you will see a list of available notification events. You can subscribe to the events that are most relevant to your workflow. For example:
   * **Document Verification Complete:** Receive an alert only when a document verification is finished. This is highly useful for teams that need to perform manual reviews of submitted documents.
   * **New User Registered:** Get notified every time a new user signs up.
   * **Verification Status Changed:** Stay updated on every change in a verification's lifecycle.
4. **Save Your Settings:** After configuring your webhook and event subscriptions, click **Update Settings** to save the configuration.

Your Slack integration is now active! Notifications for the events you subscribed to will be sent to your designated Slack channel, providing your team with timely and actionable updates.

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>
