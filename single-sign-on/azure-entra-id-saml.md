---
description: Setup SSO with Entra using a custom app for SAML authentication.
---

# Azure Entra ID SAML

1. Add a Custom Enterprise App - [https://entra.microsoft.com/#view/Microsoft\_AAD\_IAM/StartboardApplicationsMenuBlade/\~/AppAppsPreview](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/~/AppAppsPreview)
2. Go to **+ New Application** > **Create your Own application** from the top navigation menu.&#x20;
3.  Click **Integrate any other application you don't find in the gallery (Non-gallery)** radio to create a new application.

    From the next screen, fill in the following fields:

    * **App Name -** Trust Swiftly
    * **Upload Logo -** You can download [https://app.trustswiftly.com/assets/images/icon.png](https://app.trustswiftly.com/assets/images/icon.png) and use as an icon or download the below. Go to **Properties** of the app then you can modify the logo.&#x20;

    <figure><img src="../.gitbook/assets/trustswiflty-icon.png" alt="" width="188"><figcaption></figcaption></figure>


4. In the **Manage** section of the app select **Single sign-on** then click the **SAML** box.
5. Click **Edit** next to the Basic SAML Configuration

<pre class="language-html"><code class="lang-html"><strong>https://app.rippling.com/api/platform/sso/idp-metadata/XXXXXXXXXXXXXX
</strong></code></pre>



5. Paste it in your Trust Swiftly Auth settings /settings/auth and save it.
6. In Rippling for the paste the Trust Swiftly metadata URL&#x20;

```
https://[COMPANY].trustswiftly.com/auth/saml2/metadata
```

7. Edit the app for advanced SSO configuration to match the below settings. Make sure SP initiated login is checked.&#x20;

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
