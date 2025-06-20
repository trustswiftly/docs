---
description: >-
  To integrate Trust Swiftly with Wordpress it can be done in a similar manner
  as the HTML integration and link.
---

# Integrating with WordPress

We provide two primary methods for integrating Trust Swiftly into your WordPress site. The best method depends on whether you are running a WooCommerce store or a different type of site.

* **For WooCommerce Stores:** Our official plugin is the fastest and easiest way to verify customer identities before or after checkout.
* **For Other WordPress Sites:** A custom code snippet can be used to add a verification button for your logged-in users.

***

## Method 1: WooCommerce Plugin (Recommended)

Our official plugin for WooCommerce allows you to seamlessly integrate identity verification into your checkout process. You can require users to verify their identity before they can complete a purchase, or trigger a verification check after an order is placed.

This is the recommended method for all WooCommerce stores.

**Key Features:**

* Gate checkout until a user's identity is verified.
* Automatically trigger verification checks after an order is submitted.
* Display a user's verification status in their "My Account" page.
* Simple setup with no custom coding required.

**Installation & Setup**

1. **Install the Plugin:** From your WordPress dashboard, navigate to **Plugins > Add New**. Search for "**Trust Swiftly Verification**" and click "Install Now," then "Activate."
2. **Enter Your API Credentials:** Go to **WooCommerce > Settings > Trust Swiftly**. Enter your **API Key** and **Webhook Signing Secret**. You can find these in your Trust Swiftly dashboard under **Settings**.
3. **Configure:** Set your preferences for when to require verification (e.g., before or after checkout).

For a full guide and to download the plugin, visit the official WordPress.org repository.

[View Official WooCommerce Plugin](https://wordpress.org/plugins/trust-swiftly-verification/)

***

## Method 2: Custom Integration for Non-WooCommerce Sites

If you are not using WooCommerce or need a more custom implementation (e.g., for a membership site, online course, or custom user profiles), you can add a dynamic verification button using a custom **shortcode**.

This method will automatically generate a verification button for any user who is logged into your WordPress site. It uses WordPress's built-in caching system to ensure it doesn't slow down your site.

**Step 1: Add the Code to `functions.php`**

Copy the entire PHP code block below and add it to the `functions.php` file of your active WordPress theme. You can do this by navigating to **Appearance > Theme File Editor** from your dashboard.

```php
<?php
/**
 * Trust Swiftly: Creates a shortcode [trust_swiftly_button] to display a verification button
 * for the currently logged-in user. Caches the link for 12 hours.
 */
function trust_swiftly_verification_button_shortcode() {
    if ( ! is_user_logged_in() ) {
        return ''; // Don't show anything if the user is not logged in.
    }

    $current_user = wp_get_current_user();
    $user_id = $current_user->ID; // Using WordPress User ID as the reference_id

    $transient_key = 'trust_swiftly_magic_link_' . $user_id;
    $cached_link = get_transient( $transient_key );

    if ( false !== $cached_link ) {
        $magicLink = $cached_link;
    } else {
        $apiKey = 'YOUR_API_KEY'; // <-- PASTE YOUR API KEY HERE

        $url = 'https://app.trustswiftly.com/api/users/ref/' . $user_id;
        $args = [ 'headers' => [ 'Authorization' => 'Bearer ' . $apiKey, 'Accept' => 'application/json' ] ];
        $response = wp_remote_get( $url, $args );

        if ( is_wp_error( $response ) || 200 !== wp_remote_retrieve_response_code( $response ) ) {
            return '<!-- Trust Swiftly: Error retrieving link. -->';
        }

        $body = wp_remote_retrieve_body( $response );
        $data = json_decode( $body, true );
        $magicLink = $data['magic_link'] ?? '';
        
        if ( ! empty( $magicLink ) ) {
            set_transient( $transient_key, $magicLink, 12 * HOUR_IN_SECONDS );
        }
    }

    if ( ! empty( $magicLink ) ) {
        return '<a href="' . esc_url( $magicLink ) . '" class="trust-swiftly-button">Start Identity Verification</a>';
    }

    return '';
}

// Register the shortcode so WordPress recognizes it.
add_shortcode( 'trust_swiftly_button', 'trust_swiftly_verification_button_shortcode' );
?>
```

**Warning:** Always be careful when editing `functions.php`. A syntax error can cause issues with your site.

**Step 2: Add the Shortcode to Your Page**

Edit any page where you want the button to appear (e.g., a "My Profile" or "Account Details" page). Add a **Shortcode** block and type in:

`[trust_swiftly_button]`

When a logged-in user views this page, they will see their personal verification button. Logged-out users will see nothing.

**Step 3: Style the Button**

Use the CSS on our Button & Link page to style the button to match your site's branding.
