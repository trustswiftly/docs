---
description: >-
  For added security Trust Swiftly is compatible with Azure SSO which allows
  your admins to not reenter their password to access the app. Setup SSO with
  Entra using a custom app for SAML authentication.
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
5. Click **Edit** next to the Basic SAML Configuration. Then copy and paste the below into their respective inputs. Click Save to complete. Replace \[COMPANY] with your actual name.

```html
https://[COMPANY].trustswiftly.com/auth/saml2
https://[COMPANY].trustswiftly.com/auth/saml2/callback
https://[COMPANY].trustswiftly.com/auth/saml2/login
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

6. In the **Attributes & Claims** section click Edit. On this popup edit the Unique User Identifier (Name ID) so the identifier format is set to **Email address.**

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

7. Next update the **Claim name:** _name_ by clicking the edit icon and changing the value to **user.displayname**

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

8. In the SAML Certificates section copy the App Federation Metadata Url and paste it in your Trust Swiftly Auth settings page `https://[COMPANY].trustswiftly.com/settings/auth` and save it for the Single Sign On input.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

9. After this is completed and tested you can enable the Force SAML setting for added security. Only SAML authenticated sessions will be allowed.&#x20;
