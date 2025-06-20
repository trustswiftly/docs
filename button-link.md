---
description: >-
  The button integration with a link is another simple integration that allows
  for faster page loading and minimal setup.
---

# Button Link

## Implementing the Verification Button

To start the verification flow, you will present the user with a button or link on your website. This element will use the unique magic\_link generated for that user.

This guide covers the full process: retrieving the link from your backend and displaying it on your frontend as a clickable button.

## Overview Steps

1. [Create a user](https://docs.trustswiftly.com/users#create-user) with our API with the information to verify.
2. Save the `magic_link` parameter to use for your button `href` value.
3. _(Optional)_ [Regenerate the magic link](https://docs.trustswiftly.com/api/users#get-magic-link) for page refreshes or logins where the link is expired.
4. Display a button with the magic link. Recommended to use `target="_blank"` ([Example Bootstrap Button](https://www.tutorialrepublic.com/twitter-bootstrap-button-generator.php))
5. _(Optional)_ Setup redirect URL and messages. You can direct users back to your website upon verification completion to inform them of next onboarding steps.
   1. `https://{sub-domain}.trustswiftly.com`**`/settings`**

Example code

```markup
<a class="btn btn-primary" href="https://demo1.trustswiftly.com/security-verify?expires=1622216986&key=17fwnw4Nux6JbVS3RePdDK6n41s2RGQTFXPP2Nj1AZ3ZKnPDD60RQ&signature=ea4da5121e023df8a9c7dfbfa715a56dc1ee3e55e5ef0d7e4986f22a72fb7cc2" target="_blank" role="button">Verify me</a>
```

![Example Verification Button](<.gitbook/assets/image (19).png>)

## Button Assets

{% file src=".gitbook/assets/png-trust-swiftly.zip" %}
PNG Button Images
{% endfile %}

{% file src=".gitbook/assets/svg-trust-swiftly.zip" %}
SVG Button Images
{% endfile %}

![Branded Trust Swiftly Buttons](.gitbook/assets/button-group.png)



## Detailed Button Example

#### Step 1: Get the Magic Link from Your Backend

First, your server-side code needs to make an API call to Trust Swiftly to get the user's `magic_link`. You should trigger this when you need to display the button—for example, when rendering the user's profile page.

Here is a PHP example demonstrating how to get the link for a user with the `reference_id` of 'user\_12345'.

```php
<?php
// Your Trust Swiftly API Key and User's Reference ID
$apiKey = 'YOUR_API_KEY';
$referenceId = 'user_12345'; // The ID of the user in your system

// Make the API call to get user details
$url = 'https://app.trustswiftly.com/api/users/ref/' . $referenceId;
$options = [
    'http' => [
        'header' => "Authorization: Bearer " . $apiKey . "\r\n" .
                    "Accept: application/json\r\n",
        'method' => 'GET',
    ],
];
$context = stream_context_create($options);
$responseJson = file_get_contents($url, false, $context);

// Decode the JSON response and extract the magic_link
$responseData = json_decode($responseJson, true);
$magicLink = $responseData['magic_link'] ?? '#'; // Default to '#' if not found

// Now the $magicLink variable is ready to be used in your HTML.
?>
```

***

#### Step 2: Display the Button on Your Frontend

With the `$magicLink` variable available, you can now render the button. We provide a default CSS class, `.trust-swiftly-button`, to make a standard link look like a clean, modern button.

**Method A: For PHP / Server-Rendered Pages**

If your frontend is rendered with PHP, you can inject the variable directly into the `href` attribute of an `<a>` tag.

**HTML & PHP:**

```html
<!-- Use the PHP variable for the href attribute. -->
<!-- Using htmlspecialchars is a good security practice. -->
<a href="<?php echo htmlspecialchars($magicLink); ?>" class="trust-swiftly-button">
  Start Identity Verification
</a>
```

**Method B: For JavaScript / Single-Page Applications (SPAs)**

If you have a separate frontend (like React or Vue), you'll fetch the link from your own backend API and then dynamically update the button.

**HTML:**

```html
<!-- Give the button an ID so you can easily select it with JavaScript -->
<a id="verify-button" href="#" class="trust-swiftly-button">
  Start Identity Verification
</a>
```

**JavaScript:**

```javascript
// This function fetches user data from your own backend API
async function populateVerificationLink() {
  try {
    // This endpoint on YOUR server should return the magic_link
    const response = await fetch('/api/get-verification-link?userId=user_12345');
    const data = await response.json();

    if (data.magic_link) {
      const button = document.getElementById('verify-button');
      button.href = data.magic_link;
    }
  } catch (error) {
    console.error('Failed to get verification link:', error);
  }
}

// Call the function when the page loads
document.addEventListener('DOMContentLoaded', populateVerificationLink);
```

***

#### Step 3: Style the Link as a Button

To use our default button styling, add the following CSS class to your stylesheet. You can, of course, customize the colors to match your brand.

**Where to put this CSS?** You can add this to your main `.css` file or place it inside a `<style>` tag in the `<head>` of your HTML document.

```css
.trust-swiftly-button {
    background-color: #007bff; /* Primary Blue */
    color: #ffffff;            /* White Text */
    padding: 12px 24px;
    border-radius: 6px;
    text-decoration: none;      /* Removes the underline from the link */
    font-family: sans-serif;
    font-size: 16px;
    font-weight: bold;
    display: inline-block;      /* Allows padding and other box model properties */
    border: none;
    cursor: pointer;
    transition: background-color 0.2s ease-in-out;
}

.trust-swiftly-button:hover {
    background-color: #0056b3; /* A darker blue for hover */
}
```

#### Alternative: Using a `<button>` Element

If you prefer to use a semantic `<button>` tag instead of an `<a>` tag, you can use a small amount of JavaScript to trigger the navigation.

**HTML:**

```html
<button id="verify-js-button" class="trust-swiftly-button">
  Start Identity Verification
</button>
```

**JavaScript:**

```javascript
const magicLink = "THE_MAGIC_LINK_FROM_YOUR_API_CALL"; // Get this from your backend

document.getElementById('verify-js-button').addEventListener('click', () => {
  window.location.href = magicLink;
});
```
