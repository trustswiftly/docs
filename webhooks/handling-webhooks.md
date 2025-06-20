# Setup and Handling Webhooks

## Add Webhook Endpoint

1. The first step to receiving webhooks is to enable it in your settings page. `https://{sub-domain}.trustswiftly.com/settings/webhooks`
2. Click the Add Webhook button and select the events to subscribe to. You can visit [https://webhook.site/](https://webhook.site) and receive a unique url if you want to test the webhook events.

![](<../.gitbook/assets/image (10) (1).png>)

## Key Considerations

For each event occurrence, Trust Swiftly POSTs the WebHook data to your endpoint in JSON format. The full event details are included and can be used directly after parsing the JSON into an Event object. Thus, at minimum, the WebHook endpoint needs to expect data through a POST request and confirm successful receipt of that data. Beyond those two concepts, you should also follow these best practices.

**Return a 2xx status code quickly**

To acknowledge receipt of an event, your endpoint must return a 2xx HTTP status code to Trust Swiftly. All response codes outside this range, including 3xx codes, indicate to Trust Swiftly that you did not receive the event.

**Signature Verification**

Your app must verify that notification messages originated from Trust Swiftly, where not altered or corrupted during transmission, where targeted for you, and contain a valid signature. For each WebHook that is sent we also include a HTTP header for you to validate against to ensure the data we send is the data you're receiving. The `webhook_secret` is a separate secret from your API and is uniquely generated to verify the signature.

```
// payload is the array passed to the `payload` method of the webhook
// secret is the string given to the `signUsingSecret` method on the webhook.

$payloadJson = json_encode($payload); 

$signature = hash_hmac('sha256', $payloadJson, $webhook_secret);
```

![View Webhook Secret](<../.gitbook/assets/image (30).png>)

![Example header with signature](<../.gitbook/assets/image (31).png>)

## Webhook Actions

To test, view logs, edit or delete a webhook click on one of the action buttons. Sending a test webhook can be useful for debugging your setup.

![](<../.gitbook/assets/image (32).png>)

## Handling Webhooks Reliably

Once you have configured your webhook endpoint and are [verifying signatures](code-examples.md), the next step is to process the incoming data reliably. A well-built webhook consumer is fast, resilient to duplicate events, and does not depend on the order in which events are received.

The best practice for achieving this is to follow a simple but powerful pattern: **Acknowledge First, Process Later.**

This means your public-facing webhook endpoint should do the absolute minimum amount of work required before telling Trust Swiftly that the event was received. Any complex business logic should be handed off to a background process.

The first step to adding WebHooks to your account is to build your own custom endpoint. Creating a WebHook endpoint on your server is no different from creating any page on your website. With PHP, you might create a new .php file on your server; with a Ruby framework like Sinatra, you would add a new route with the desired URL.
