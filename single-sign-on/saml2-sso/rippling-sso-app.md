---
description: Setup SSO with Rippling using a custom application
---

# Rippling SSO App

1. Add a Custom App in Rippling.&#x20;
2. Go to **IT Management** > **Custom App** from the left navigation menu.&#x20;
3.  Click **Create New App** button to create a new application.

    From the next screen, fill in the following fields:

    * **App Name -** TrustSwiftly
    * **Select Categories**&#x20;
    * **Upload Logo -** You can download [https://app.trustswiftly.com/assets/images/icon.png](https://app.trustswiftly.com/assets/images/icon.png) and use as an icon or download the below.

    <figure><img src="../../.gitbook/assets/trustswiflty-icon.png" alt="" width="188"><figcaption></figcaption></figure>

    * **What type of app would you like to create?** - Make sure you select **Single Sign-On (SAML)** from the list.

    \

4. Copy the IdP Metadata URL from Rippling. i.e. similar too

<pre class="language-html"><code class="lang-html"><strong>https://app.rippling.com/api/platform/sso/idp-metadata/XXXXXXXXXXXXXX
</strong></code></pre>

5. Paste it in your Trust Swiftly Auth settings /settings/auth and save it.
6. In Rippling for the paste the Trust Swiftly metadata URL&#x20;

```
https://[COMPANY].trustswiftly.com/auth/saml2/metadata
```

7. Edit the app for advanced SSO configuration to match the below settings. Make sure SP initiated login is checked.&#x20;

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
