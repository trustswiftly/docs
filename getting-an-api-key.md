---
description: To access the Trust Swiftly API, you'll need an API key.
---

# Getting an API Key

When you're ready to use the API in production using live data you can generate an API key in the menu for **Developer** settings. You must click Create Token and provide a name to track it.

{% hint style="warning" %}
**Keep your keys secure**

Your API keys carry many privileges, so be sure to keep them secure! Do not share your secret API keys in publicly accessible areas such as GitHub, client-side code, and so forth.
{% endhint %}

#### API Keys & Authentication

All API requests to the Trust Swiftly platform are authenticated using a secret API key. Think of this key as a unique password that identifies your application and grants it access to your account data.

You must include this key in every API request. Access to the API is only available on our paid plans.

**How to Generate Your API Key**

You can generate and manage your API keys from your Trust Swiftly dashboard.

1. Log in to your [Trust Swiftly Dashboard](https://app.trustswiftly.com/).
2. Navigate to **Settings** in the main menu, then select the **API** tab.
3. Click the **Generate New Key** button.
4. A new secret key will be generated for you.

![Token Creation Process](<.gitbook/assets/image (18).png>)

> **Important: Copy Your Key Immediately**> \
> For your security, your secret API key is **only displayed once** at the time it is created. You must copy it and store it in a secure password manager or other secret store immediately. If you lose the key, you will need to revoke it and generate a new one.

***

#### Keeping Your API Key Secure

Your API key grants full access to your Trust Swiftly account data. You must treat it with the same care as you would a password.

**Security Best Practices:**

* **Do Not Share It:** Never share your key publicly, in client-side code, or in public code repositories like GitHub.
*   **Use Environment Variables:** The best practice is to store the key in an environment variable on your server and load it into your application from there. This prevents the key from being hard-coded into your application source code.

    **Example:**

    ```bash
    # Set the environment variable on your server
    export TRUST_SWIFTLY_API_KEY="your_secret_key_goes_here"
    ```
* **Revoke Compromised Keys:** If you suspect a key has been exposed or compromised, go to the API settings page immediately and revoke it. Then, generate a new key and update your application.

***

#### What's Next?

Now that you have your API key, you're ready to make your first API call.

* **Quickstart Guide**: Follow our guide to create your first user and see the full workflow in action.
* **Create a User**: Dive straight into the API reference for creating and managing users.
