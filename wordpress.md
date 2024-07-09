---
description: >-
  To integrate Trust Swiftly with Wordpress it can be done in a similar manner
  as the HTML integration and link.
---

# WordPress

## WooCommerce Plugin

Our plugin for WooCommerce can be used to verify identities before and after checkout for basic verifications. [https://wordpress.org/plugins/trust-swiftly-verification/](https://wordpress.org/plugins/trust-swiftly-verification/)

For other integrations with Wordpress custom code is advised to create users.&#x20;

## Sample WordPress Code

Example code can be copied into functions.php which allows for using a shortcode to generate a verification link \[trustlink]

```php
add_shortcode('trustlink', 'generate_trustlink');
function generate_trustlink(){
    if ( is_user_logged_in() ) {
        $user_id=get_current_user_id();
        $metaData=json_decode(get_user_meta($user_id,'trust_user_data',true));
        $endpoint = 'https://test.trustswiftly.com/api/v1/users/'.$metaData->id.'/verify-url';
        $user_info = get_userdata($user_id);
        $user_email = $user_info->user_email;
        $body = [
            'email' => $user_email,
        ];

        $body = wp_json_encode($body);

        $options = [
            'body' => $body,
            'headers' => [
                'Authorization' => 'Bearer $api_key',
                'Content-Type' => 'application/json',
            ],
            'returntranser' => true,
            'timeout' => 60,
            'redirection' => 10,
            'data_format' => 'body',
        ];

        $response = wp_remote_post($endpoint, $options);
        $responseData=json_decode($response['body']);
        return $responseData->short_url;
    }else{
        return false;
    }
}
add_action('user_register', function ( $user_id ) {
    $endpoint = 'https://test.trustswiftly.com/api/v1/users';
    $user_info = get_userdata($user_id);
    $user_email = $user_info->user_email;
    $body = [
        'email' => $user_email,
    ];

    $body = wp_json_encode( $body );

    $options = [
        'body'        => $body,
        'headers'     => [
                'Authorization'=>'Bearer $api_key',
                'Content-Type' => 'application/json',
        ],
        'returntranser'=>true,
        'timeout'     => 60,
        'redirection' => 10,
        'data_format' => 'body',
    ];

    $response =wp_remote_post( $endpoint, $options );

    add_user_meta( $user_id, 'trust_user_data', $response['body'],true);
});
```
