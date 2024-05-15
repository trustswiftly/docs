---
description: >-
  Setup SAML2 authentication for your Trust Swiftly instance. This adds
  additional safeguards to access the admin dashboard and quicker onboarding for
  your team by centralizing user management.
---

# SAML2 SSO (Okta, etc)

### Adding Trust Swiftly to Okta

1. Log in to your Okta organization as a user with administrative privileges.
2. Click Applications in the menu bar. Then click Add Application and then Create New App.
3. In the Create a New Application Integration dialog box, leave Web as the platform and select SAML 2.0 as the protocol. Click Create.
4. On (1) General Settings, enter Trust Swiftly as the name of the new Application. Click Next
5. On (2) Configure SAML, enter the following for the fields. Click Next and then leave any feedback.
   * Single sign on URL: `https://{subdomain}.trustswiftly.com/auth/saml2/callback`
   * Audience URI: `https://{subdomain}.trustswiftly.com/auth/saml2`
   * Attribute Statements
     * Name: email
     * Name format: Unspecified
     * Value: user.email
   * Get your Identity Provider metadata XML URL for Trust Swiftly to integrate back with Okta. This can be found under the Sign On tab in the SAML 2.0 callout by clicking the Identity Provider metadata link. Copy the URL and keep it handy for the next steps. The format of the URL should look like `https://dev12345.okta.com/app/4343431a/sso/saml/metadata`

![](<../../.gitbook/assets/image (38).png>)

### Completing the Okta integration in Trust Swiftly

1. Log in to your Trust Swiftly dashboard as a user with Admin permissions and go to the Auth & Registration page under settings.
2. Enter in the Metadata URL you obtained from the last step in the Adding Trust Swiftly to Okta section. Then click Update Settings.

### Logging in to Trust Swiftly through Okta

1. To log in to Trust Swiftly through Okta, first make sure that the user has been assigned to the Application in Okta.
2. The user should then see Trust Swiftly in their Okta dashboard. By clicking Trust Swiftly, they should automatically log in to their Trust Swiftly dashboard.
