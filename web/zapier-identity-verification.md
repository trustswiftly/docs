---
description: >-
  Integrating Trust Swiftly with Zapier allows you to automate identity
  verification processes seamlessly across various apps and services, enhancing
  security and efficiency without the need for coding.
---

# Zapier Identity Verification

### **Set up your identity verification workflow automation with Zapier**

Ensuring trust in digital products is increasingly crucial. One effective method is using an identity verification solution like Trust Swiftly. With Trust Swiftly, you can authenticate users' true identities and effortlessly integrate the service with various apps and platforms via Zapier. This guide will demonstrate how to create automated workflows for identity verification, featuring biometric authentication, KYC, AML and ID verification, that seamlessly connect with spreadsheets, databases, communication tools, and CRMs. This no-code/low-code solution is accessible to both developers and non-technical users alike.

### **Prerequisites:**

* You need a Trust Swiftly account. If you don’t have one, navigate and [create one here](https://app.trustswiftly.com/create)
* A Zapier Account

#### **Step 1: Sign Up or Log In to Zapier**

1. Go to [Zapier’s website](https://zapier.com/).
2. If you don’t have an account, click on [**Sign Up**](https://zapier.com/sign-up) and create one. If you already have an account, click on [**Log In**](https://zapier.com/app/login).

#### **Step 2: Access Trust Swiftly on Zapier**

1. Once logged in, navigate to the [Trust Swiftly Zapier Integrations page](https://zapier.com/apps/trust-swiftly/integrations).
2. Click on an example connection [**Connect a new account**](https://zapier.com/apps/trust-swiftly/integrations/google-sheets) and search for **Trust Swiftly**.

#### **Step 3: Set Up a New Zap**

1. Click on [**Make a Zap**](https://zapier.com/app/zaps) to start creating a new Zap.

![](<../.gitbook/assets/0 (2).png>)

1. Choose **Trust Swiftly** as your **Action**

![](<../.gitbook/assets/1 (2).png>)

#### **Step 4: Configure the Trigger**

1. Select a **Trigger Event** from the available options (e.g., **Get Verification Status**).
2. Click **Continue** and follow the prompts to connect your Trust Swiftly account. You will need your API Key and your URL i.e. \[mycompany].trustswiftly.com
3. Test the trigger to ensure it’s working correctly.

#### **Step 5: Choose an Action App**

1. After setting up the trigger, choose an **Action App** (e.g., Google Sheets, Slack).
2. Select an **Action Event** (e.g., **Create Spreadsheet Row** in Google Sheets).

#### **Step 6: Configure the Action**

1. Connect your chosen Action App account.
2. Set up the action by mapping the data from Trust Swiftly to the fields in your Action App. You can use dynamic data to set the email of the user. The template ID is used to set which verifications the user sees for example ID and Selfie.

![](<../.gitbook/assets/2 (2).png>)

1. Test the action to ensure it works as expected.

#### **Step 7: Finalize and Turn On Your Zap**

1. Review your Zap setup.
2. Click **Turn on Zap** to activate it.&#x20;

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

#### **Step 8: Receive Webhooks in Zapier**

Using a [Zapier catch hook](https://help.zapier.com/hc/en-us/articles/8496288690317-Trigger-Zaps-from-webhooks) trigger allows you to receive any status updates from Trust Swiftly and create advanced configurations with thousands of integrations. You can quickly create using a [pre-filled Zap](https://api.zapier.com/v1/embed/trust-swiftly/create?steps\[0]\[app]=WebHookAPI\&steps\[0]\[action]=hook\_v2\&steps\[1]\[app]=App210840CLIAPI@latest\&steps\[1]\[action]=identity\_verification\&steps\[1]\[params]\[email]=ACTION\_EMAIL).

1. Edit your Zap and add a trigger. Search for **Webhooks by Zapier.** Then select a Catch Hook.

![](<../.gitbook/assets/4 (2).png>)

1. Copy the Webhook URL i.e. [https://hooks.zapier.com/hooks/catch/123/111pt7tt/](https://hooks.zapier.com/hooks/catch/123/111pt7tt/)
2. Go to the Developer section in the Trust Swiftly Admin and [Setup and Handling Webhooks.](https://docs.trustswiftly.com/webhooks/handling-webhooks) Paste the webhook URL into it and select an event to receive notifications about.

![](<../.gitbook/assets/5 (2).png>)

1. Test the webhook after you completed a test verification. The results will show similar as below depending on the method you completed.

![](<../.gitbook/assets/6 (2).png>)

1. You can use the webhook data for subsequent steps by clicking the **+** icon and add another action such as sending a notification in a chat app or adding it to a database. Multiple steps can be used together to create complex automations.&#x20;

![](<../.gitbook/assets/7 (2).png>)

#### **Example Use Cases**

**Scenario**: Automatically log verification statuses in a various apps or trigger verifications from other apps.

1. **Trigger**: Trust Swiftly - Get Verification Status.
2. **Action** : Google Sheets - Create Spreadsheet Row.
3. **Databases:** Airtable, Firebase, PostgresSQL
4. **Communication Tools:** Discord, Gmail, Sendgrid, Mailchimp
5. **CRMs:** Hubspot, Salesforce, Pipedrive

By following these steps, you can seamlessly integrate Trust Swiftly with various apps on Zapier to automate your workflows and save time. Check out more possibilities for integrations by viewing [Explore All Apps | Zapier](https://zapier.com/apps).
