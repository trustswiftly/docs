---
description: >-
  This integration guide is for setting up our embedded verification option.
  Complete the prerequisites before integrating the flow.
---

# Integration

## [**Alternate Integration Methods**](./)

## **Prerequisites**

### Step 1

Following the account creation, create your branded verification site for verifying your users. Your users will be verified on this URL for hosted integrations.

**Parameter to Note: `baseUrl`**

![](<.gitbook/assets/image (20).png>)

### Step 2

Create a template(s) for required verification(s) to assign to your users. You can create multiple templates and then use those templates as conditions to invoke multiple verification combinations to your users when they are created or trigger a risk action.

**Parameter to Note: `template_id`**

![Click Add Template](<.gitbook/assets/image (21).png>)

![Input the name and enable each verification assigned to the template](<.gitbook/assets/image (22).png>)

### Step **3** <a href="#step-2" id="step-2"></a>

Generate your API keys by going to the Settings -> Developer, click on the create key to generate your key.

![Click Create API Key](<.gitbook/assets/image (23).png>)

The keys are only visible once so please copy and save the keys.

**KEY (`api_key`) :** This key will be used for API calls which are done through the server of your applications. For example: [Create User API](users.md#create-user)

![Created keys to save](<.gitbook/assets/image (24).png>)

***

#### Displaying the User Verification Flow

Once you have created a user via the API, the next step is to present them with the verification flow. Trust Swiftly uses a secure, unique **Magic Link** for this process. This link directs the user to a dedicated page to complete their verification steps.

There are two primary ways to present this flow to your users, both of which use the same core Magic Link technology.

***

#### Core Technology: The Magic Link

When you create a user, the API response contains a `magic_link`:

```json
{
  "id": "usr_abcde12345",
  "reference_id": "user_12345",
  // ... other fields
  "magic_link": "https://verify.trustswiftly.com/v/abcdef123456"
}
```

This URL is the entry point for the user's verification journey. You can guide what happens after completion by providing a `redirect_url` when you create the user. This is the **most critical step** for creating a seamless user experience.

**Example API call with redirect:**

```bash
curl -X POST https://company.trustswiftly.com/api/users \
  -H "Authorization: Bearer YOUR_API_KEY" \
  # ... other headers
  -d '{
    "reference_id": "user_12345",
    "email": "test@example.com",
    "redirect_url": "https://yourapp.com/verification-complete"
  }'
```

When the user finishes, they will be sent to:`https://yourapp.com/verification-complete?reference_id=user_12345&status=completed`

Now, let's look at how to use this link.

***

#### Method 1: Standard Web Redirect

This is the simplest method and is ideal for any web application. The user is redirected from your site to the verification page and then redirected back upon completion.

**How it works:**

1. Your user clicks a "Start Verification" button on your website.
2. This button links to the `magic_link` you received from the API.
3. The user completes the steps on the secure verification page.
4. After completion, they are automatically redirected back to the `redirect_url` you specified.

**Example HTML:**

```html
<!-- Get the magic_link from your backend and render it in the link's href -->
<a href="THE_MAGIC_LINK_FROM_THE_API_RESPONSE" class="button">
  Start Identity Verification
</a>
```

***

#### Method 2: Embedding in a Mobile App (Full Webview)

This method is ideal for providing a seamless experience within your native iOS or Android application. The verification flow is opened in an in-app browser (a "webview").

The process is nearly identical to the web redirect, but your native app must listen for the final redirect to know when the process is complete.

**How it works:**

1. Your mobile app gets a `magic_link` from your backend (which includes the `redirect_url`).
2. A user taps a "Start Verification" button in the app.
3. The app opens the `magic_link` in a full-screen webview.
4. The user completes the verification steps within the webview.
5. When finished, the webview will be redirected to your `redirect_url`.
6. Your native app code should **intercept this specific navigation event**. When it detects the webview navigating to your `redirect_url`, it knows the user is done and can programmatically close the webview and refresh the native UI.

This prevents the user from being "stuck" in the webview and provides a smooth transition back to your app's native experience.

***

#### Customization: Whitelabeling & Custom Domains

To create a truly integrated experience, you can remove all Trust Swiftly branding and host the verification flow on your own custom domain.

* **Remove Branding:** Replace the Trust Swiftly logo with your own.
* **Custom Domain:** Instead of `verify.trustswiftly.com`, the user will see a URL like `verify.yourdomain.com`.

This powerful feature gives your users confidence that they are still within your trusted ecosystem.

To configure this, navigate to **Settings > Branding** in your Trust Swiftly dashboard.



