---
description: >-
  Zoho Cliq can be used to receive notifications from Trust Swiftly about
  verification statuses.
---

# Zoho Cliq

**Configuring Zoho Cliq Notifications**

Integrate Trust Swiftly with Zoho Cliq to receive real-time notifications about verification events. This allows your team to monitor statuses directly within your Cliq channels, ensuring prompt awareness and action.

This integration requires creating a custom bot in Zoho Cliq to handle incoming messages from Trust Swiftly.

**Step 1: Create a Bot and Incoming Webhook in Zoho Cliq**

First, you need to set up a bot in Zoho Cliq that will receive and post the notifications.

1. **Follow the Zoho Cliq Guide:** Use Zoho's official guide to create a bot with an "Incoming Webhook Handler." You can find the detailed steps here: [Zoho Cliq - Incoming Webhook Handler Guide](https://help.zoho.com/portal/en/community/topic/cliq-bots-get-notifications-about-any-action-on-an-application-with-the-incoming-webhook-handler).
2. **During Setup, You Will:**
   * **Create a Bot:** Give your bot a descriptive name, like "Trust Swiftly," and an icon for easy identification.
   * **Enable the Incoming Webhook Handler:** This is the core component that allows the bot to receive external data.

**Step 2: Configure the Bot's Handler Code**

The handler determines how the bot processes and displays the information it receives from Trust Swiftly.

1. In your bot's settings, navigate to the **Code** or **Handler** section.
2. Delete any placeholder code and paste the following code snippet into the editor. This code is pre-configured to format Trust Swiftly's notifications into readable messages.

```javascript
// Incoming Webhook Handler Code for Trust Swiftly
response = Map();
verification_name = body.get("verification_name");
email = body.get("email");
user_url = body.get("user_url");
user_id = body.get("user_id");
status = body.get("verification_status");
first_name = body.get("first_name");
last_name = body.get("last_name");
phone = body.get("phone");
date = body.get("date");
userids = body.get("userids");
verification_data = body.get("verification_data");

// This block handles general verification updates.
if(body.get("userids") == null)
{
	response = {"text":"A new verification was updated: \n Method: " + verification_name + " \n Data: " + verification_data + " \n Email: " + email + "\n Phone: " + phone + " \n User ID:" + user_id + "\n [View User URL](" + user_url + ") \n Status: " + status + " \n Date: " + date,"card":{"title":"Verification Update","theme":"modern-inline"},"buttons":{{"label":"View Details","type":"+","action":{"type":"open.url","data":{"web":user_url}}}}};
	response.put('bot',{"name":"Trust Swiftly","image":"https://trustswiftly.com/assets/img/favicon.png"});
	
    // IMPORTANT: Change 'trustswiftly' to your desired channel's unique name.
	zoho.cliq.postToChannelAsBot('trustswiftly','trustswiftly',response);
	return response;
}
// This block handles notifications that require a specific user's review.
else
{
	response = {"text":"A new verification requires review: \n " + verification_data + " \n Email: " + email + "\n Phone: " + phone + " \n User ID:" + user_id + "\n [View User URL](" + user_url + ") \n Reviewer: " + userids,"card":{"title":"Verification Update","theme":"modern-inline"},"buttons":{{"label":"View Details","type":"+","action":{"type":"open.url","data":{"web":user_url}}}}};
	response.put('bot',{"name":"Trust Swiftly","image":"https://trustswiftly.com/assets/img/favicon.png"});
	response.put("userids",userids);
	return response;
}
```

3. **Important:** In the code above, locate the line `zoho.cliq.postToChannelAsBot('trustswiftly', ...);`. You **must** change the first `'trustswiftly'` to the unique name of the Zoho Cliq channel where you want the bot to post messages.
4. **Save and Publish** the handler code.

**Step 3: Get Your Unique Webhook URL**

After setting up the handler, you need to get the unique URL for Trust Swiftly to send data to.

1. In your bot's settings, find the **Incoming Webhook Endpoint**.
2. Next, go to the **Webhook Tokens** section to generate a token if one doesn't already exist.
3. Combine these pieces to form your final URL, which will look like this:   `https://cliq.zoho.com/company/{zoho_company_id}/api/v2/bots/{bot_unique_name}/incoming?zapikey={your_token}`

**Step 4: Configure Trust Swiftly**

1. In your Trust Swiftly dashboard, navigate to **Settings** -> **Notifications** and select the **Zoho Cliq** tab.
2. Paste the complete Webhook URL you constructed in the previous step into the **Webhook URL** field.
3. **Subscribe to Events** that you want to be notified about (e.g., Document Verification Complete).
4. Click **Update Settings**.

**Step 5: Add the Bot to Your Cliq Channel**

Finally, for the bot to be able to post messages, you must add it to the channel you specified in the handler code.

1. Go to the desired channel in Zoho Cliq.
2. Type `@` followed by your bot's name (e.g., `@Trust Swiftly`) and send the message.
3. Follow the prompts to add the bot to the channel.

Your integration is now complete! Notifications from Trust Swiftly will appear in your configured Zoho Cliq channel.

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption><p>Find the webhook endpoint</p></figcaption></figure>

* Add the Trust Swiftly bot to any channels you require

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>Make sure to add the bot to your channel.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Example Notification in Cliq</p></figcaption></figure>
