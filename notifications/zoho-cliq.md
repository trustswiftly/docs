---
description: >-
  Zoho Cliq can be used to receive notifications from Trust Swiftly about
  verification statuses.
---

# Zoho Cliq

### Create Bot and Setup Incoming Handler

1. Follow the below guide to setup a bot for Trust Swiftly to send notifications through Cliq: [https://help.zoho.com/portal/en/community/topic/cliq-bots-get-notifications-about-any-action-on-an-application-with-the-incoming-webhook-handler](https://help.zoho.com/portal/en/community/topic/cliq-bots-get-notifications-about-any-action-on-an-application-with-the-incoming-webhook-handler)
2. Copy and paste the below snippet for the bot to automatically post a message for the webhook.
3. Add your unique bot incoming webhook url and token. For example, first get the Incoming Webhook Endpoint and then select Webhook Tokens. You can name the bot Trust Swiftly.
4. Go to Integration Keys and add the below url to your setup. Make sure to replace with your own settings.

{% code overflow="wrap" %}
```html
https://cliq.zoho.com/company/<zoho_company>/api/v2/bots/trustswiftly/incoming?zapikey=<token>
```
{% endcode %}

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption><p>Find the webhook endpoint</p></figcaption></figure>

* Add the Trust Swiftly bot to any channels you require

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Make sure to add the bot to your channel.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Example Notification in Cliq</p></figcaption></figure>

```javascript

// Incoming Webhook Handler Code Snippet 
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
if(body.get("userids") == null)
{
	response = {"text":"A new verification was updated: \n Method: " + verification_name + " \n Data: " + verification_data + " \n Email: " + email + "\n Phone: " + phone + " \n User ID:" + user_id + "\n [View User URL](" + user_url + ") \n Status: " + status + " \n Date: " + date,"card":{"title":"Verification Update","theme":"modern-inline"},"buttons":{{"label":"View Details","type":"+","action":{"type":"open.url","data":{"web":user_url}}}}};
	response.put('bot',{"name":"Trust Swiftly","image":"https://trustswiftly.com/assets/img/favicon.png"});
	// Comment the below code if you do not have a channel called Trust Swiftly
	zoho.cliq.postToChannelAsBot('trustswiftly','trustswiftly',response);
	return response;
}
// Used for Knowledge approvals and specific user notifications
else
{
	response = {"text":"A new verification requires review: \n " + verification_data + " \n Email: " + email + "\n Phone: " + phone + " \n User ID:" + user_id + "\n [View User URL](" + user_url + ") \n Reviewer: " + userids,"card":{"title":"Verification Update","theme":"modern-inline"},"buttons":{{"label":"View Details","type":"+","action":{"type":"open.url","data":{"web":user_url}}}}};
	response.put('bot',{"name":"Trust Swiftly","image":"https://trustswiftly.com/assets/img/favicon.png"});
	response.put("userids",userids);
	return response;
}

```
