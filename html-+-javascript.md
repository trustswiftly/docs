# HTML + Javascript

## General

This document explains how to integrate the verification flow directly into your web application through our JavaScript component to **verify** the identity of your users. This stage might be at the **signup** page of your application, or at a later point to enrich the profiles of your users.

## 1. Importing the component

Start your integration by importing the Trust Swiftly embed javascript to your HTML page.

```markup
<script type="text/javascript" src="https://www.trustswiftly.local/account/trust-verify.js"></script>
```

## 2. Initialising the component

| Argument | Description |
| :--- | :--- |
| **clientToken** | The token used to identify a given user. |
| **baseUrl** | The URL used for your hosted panel. |

```markup
<button type="button" id="myButton"></button>
```

```markup
<script>
    const handler = TrustVerify.configure({
        onComplete: function() {},
        onExit: function() {},
        onDisplay: function() {},
        onStateChange: function() {},
        onError: function() {}
    });
    document.getElementById('myButton').addEventListener('click', function(e) {
        handler.open({
            clientToken: '',
            baseUrl: ''
        });
    });
</script>
```

