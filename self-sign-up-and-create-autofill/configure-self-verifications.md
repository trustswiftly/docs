# Configure self verifications

Self-verifications are a quick way to get started with Trust Swiftly. This feature allows your users to create their own accounts and complete verifications without requiring any code or integration on your part. You can always add other integration options later to further automate the process.

To configure the self-verification process, navigate to your registration settings page at `https://{sub-domain}.trustswiftly.com/settings/auth`.

**General Settings (Registration Tab)**

These settings control the core sign-up experience for your users.

* **Allow customer sign up?:** This is the primary switch to enable the self-verification page (`/signup`). This page should be shared directly with your customers.
* **Registration Password:** When disabled, it allows for a passwordless registration process. If enabled, users will be required to create a password when signing up.
* **Terms and Conditions:** Enable this to require users to agree to your terms and conditions before creating an account.
* **Email Confirmation:** When enabled, users must verify their email address before they can log in to their account.

After configuring these options, click **Update Settings** to save them.

**Verification Templates (Registration Tab)**

You can direct users to complete a specific set of verifications after they sign up.

* **Default Verification Template:** This sets a global default template for any user who signs up through the general `.../signup` URL. After creating an account, they will be prompted to complete the verifications defined in this template (e.g., ID Assist Apply).
* **Signup Verification Template URLs:** For more specific needs, you can use unique URLs that send users to a particular verification flow. This is useful if you want to give different user groups different verification tasks. For example:
  * To have a user complete only the "Reverify ID" flow, direct them to: `https://{sub-domain}.trustswiftly.com/signup/reverify-id`
  * To have them complete the "ID Assist Apply" flow, use: `https://{sub-domain}.trustswiftly.com/signup/id-assist-apply`

**Social Media Registration (Registration Tab)**

Simplify the registration process by allowing users to sign up using their existing social media accounts.

* **Social Account:** Select which social media platforms (e.g., Google, LinkedIn) users are permitted to register with.

Click **Update Settings** in this section to save your social media registration preferences.

**Customizing Signup Page Content (Signup Content Tab)**

You can add custom text and information to the top of your signup page to provide context or specific instructions to your users. This is useful for explaining the purpose of the verification, what documents are required, or setting other expectations.

To add custom content:

1. Navigate to the **Signup Content** tab.
2. Use the rich text editor to add your desired content. You can format text, add headings, and structure the information clearly.
3.  For example, you could add a notice for users who need temporary verification for a specific purpose:

    > **Welcome to our enhanced verification process for P2P crypto buyers.** To ensure the security of our marketplace and comply with KYC (Know Your Customer) regulations, we require additional verification for high-value transactions.
    >
    > Please be prepared to submit a government-issued ID and a proof of address. This one-time verification will unlock higher trading limits and help protect our community from fraud.
4. Click **Update Details** to save the content and publish it to your signup page.

**Directing Users to Verify**

Once configured, you can add a link or button on your website that directs users to the appropriate Trust Swiftly sign-up page.

**General Sign-up Link:**

```html
<a href="https://{sub-domain}.trustswiftly.com/signup" target="_blank">
Verify yourself at Trust Swiftly</a>
```

**Pre-Populating User Data**

You can make the sign-up process even easier for your users by pre-populating fields in the registration form. Add the following parameters to any of your signup URLs: `email`, `first_name`, `last_name`, and `phone`.

**Example URL with pre-populated data:**`/signup?email=test@example.com&first_name=test&last_name=test&phone=%2B13129450121`

![Options to enable for self sign up](<../.gitbook/assets/image (13) (1).png>)

Example signup page with custom content. This /signup URL can be shared for the quickest and least effort verifications.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Example Sign Up Register page</p></figcaption></figure>
