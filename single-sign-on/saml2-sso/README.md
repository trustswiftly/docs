---
description: >-
  Setup SAML2 authentication for your Trust Swiftly instance. This adds
  additional safeguards to access the admin dashboard and quicker onboarding for
  your team by centralizing user management.
---

# SAML2 SSO (Okta, etc)

Integrating Trust Swiftly with a SAML2 identity provider (IdP) like Okta, Azure AD, or others centralizes user management, enhances security, and simplifies the login process for your team. This guide will walk you through setting up SAML2 SSO.

**Step 1: Configure Your Identity Provider (Okta Example)**

First, you need to create a new application within your identity provider. The following steps use Okta as an example.

1. Log in to your Okta organization with administrative privileges.
2. Navigate to **Applications** > **Applications**, and click **Create App Integration**.
3. In the pop-up window, select **SAML 2.0** as the sign-in method and click **Next**.
4. **General Settings**: Give the application a name, such as "Trust Swiftly," and click **Next**.
5. **Configure SAML**: Enter the following values into the corresponding fields:
   * **Single sign on URL**: `https://{subdomain}.trustswiftly.com/auth/saml2/callback`
   * **Audience URI (SP Entity ID)**: `https://{subdomain}.trustswiftly.com/auth/saml2`
6. **Attribute Statements**: Configure an attribute to pass the user's email address to Trust Swiftly.
   * **Name**: `email`
   * **Name format**: `Unspecified`
   * **Value**: `user.email`
7. Click **Next**, then **Finish**.
8. **Get Metadata URL**: After creating the app, go to the **Sign On** tab. In the "SAML 2.0" section, find the link labeled **"Identity Provider metadata"**. Right-click and copy this URL, as you will need it for the next step. The URL will look something like this: `https://your-org.okta.com/app/xxxxxxxx/sso/saml/metadata`.

**Step 2: Configure Trust Swiftly**

Next, you will provide the Identity Provider details to Trust Swiftly.

1. Log in to your Trust Swiftly dashboard with an administrator account.
2. Navigate to **Settings** -> **Auth & Registration**.
3. On the **Authentication** tab, locate the **Single Sign On** section.
4. Paste the **Metadata URL** you copied from your identity provider into the text field.

**Step 3: Enforce Single Sign-On (Optional)**

For maximum security, you can require all administrators and analysts to log in exclusively through SSO, disabling password-based login for those roles.

1. While still on the **Auth & Registration** page, find the **Enforce Single Sign On** toggle.
2. Enable this option to make SSO the only permitted login method for admins and analysts.
3. Click **Update Settings** to save all your changes.

Enforcing SSO ensures that access to your Trust Swiftly instance is managed entirely through your central identity provider.

**Step 4: Logging In via SSO**

To log in, users must first be assigned the application within your identity provider (e.g., Okta).

Once assigned, users can simply click the Trust Swiftly application from their IdP dashboard. They will be automatically redirected and logged into their Trust Swiftly account without needing to enter a password.
