# Webhook Code Examples

To ensure the integrity and authenticity of the webhooks sent from Trust Swiftly, we sign every request sent to your endpoint. By verifying this signature, you can confirm that the webhook was sent by Trust Swiftly and that its payload has not been tampered with during transmission.

The signature is an HMAC-SHA256 hash, generated using your unique webhook signing secret and the raw request body. This signature is passed in the Signature HTTP header with each request.

Below are code examples demonstrating how to properly verify the webhook signature in several common languages and frameworks. It is crucial to use a secure, constant-time comparison method to prevent timing attacks.

* [JavaScript (Express.js)](code-examples.md#example-signature-verification-js)
* [Python (Flask)](code-examples.md#python-example-using-flask)
* [PHP (Laravel)](code-examples.md#laravel-php-example)
* [PHP (Procedural)](code-examples.md#example-signature-verification-php)

### Example Payload

```javascript
{
   "id":"7d2dde92-885b-4159-8772-0367e4e39b6f",
   "ip":"127.0.0.1",
   "event":"verification.pending",
   "email":"test@example.com",
   "trust_id":28,
   "created_at":"2022-01-28T21:06:44.000000Z",
   "ip_country":"US",
   "user_status":"Active",
   "reference_id":null,
   "last_activity":"2022-01-28 22:46:44",
   "verifications":[
      {
         "id":3,
         "name":"Document \/ ID",
         "status":{
            "value":1,
            "friendly":"Processing"
         },
         "attributes":{
            "workflow":"ID + Selfie"
         }
      },
      {
         "id":1,
         "name":"Email",
         "status":{
            "value":0,
            "friendly":"Assigned"
         }
      }
   ]
}
```

### Example Handling (PHP)

```php
<?php

/**
 * Procedural PHP example for verifying Trust Swiftly Webhooks.
 */

// --- 1. Configuration ---
// It is a critical security practice to store your secret outside of your codebase.
// For example, load it from an environment variable or a secure config file.
// $webhookSecret = getenv('TRUST_SWIFTLY_SECRET');
$webhookSecret = 'XXXX'; // Replace with your actual secret key.

// --- 2. Get Request Data ---

// Get the raw POST data from the request. It's crucial to use the raw body
// for the signature calculation. Read it only once and store it in a variable.
$payload = file_get_contents('php://input');
if ($payload === false || empty($payload)) {
    // This can happen if the request is not a POST or has an empty body.
    http_response_code(400);
    exit('Error: Could not read request body.');
}

// Get the signature from the request headers.
// Note: PHP typically prefixes headers with `HTTP_` and converts them to uppercase.
// 'Signature' becomes 'HTTP_SIGNATURE'.
if (!isset($_SERVER['HTTP_SIGNATURE'])) {
    http_response_code(400);
    exit('Error: Signature header is missing.');
}
$receivedSignature = $_SERVER['HTTP_SIGNATURE'];


// --- 3. Verify the Signature ---

// Compute the expected signature using HMAC-SHA256.
// This hash must be calculated on the raw, unmodified request body.
$computedSignature = hash_hmac('sha256', $payload, $webhookSecret);

// Use hash_equals() for a secure, constant-time comparison.
// This prevents timing attacks where an attacker could guess the signature character by character.
if (!hash_equals($computedSignature, $receivedSignature)) {
    http_response_code(403); // Use 403 Forbidden for invalid signatures.
    exit('Tampered Request: Invalid signature.');
}


// --- 4. Process the Payload ---

// If we reach this point, the signature is valid and the request is authentic.
// You can now safely decode and process the JSON payload.
$webhookData = json_decode($payload, true); // Using `true` decodes to an associative array.

if (json_last_error() !== JSON_ERROR_NONE) {
    http_response_code(400);
    exit('Error: Invalid JSON payload.');
}

// TODO: Add your business logic here.
// For example, log the event or update your database based on the verification status.
// A switch statement is a good way to handle different verification types.

$verifications = $webhookData['verifications'] ?? [];

foreach ($verifications as $verification) {
    $name = $verification['name'] ?? 'Unknown';
    $status = $verification['status']['friendly'] ?? 'unknown';

    // Example: Log the result
    // error_log("Received verification: {$name} - Status: {$status}");

    switch ($name) {
        case "Email":
            // Handle email verification logic
            break;
        case "Phone / SMS":
            // Handle phone verification logic
            break;
        default:
            // Handle any other verification methods
            // error_log("Received a different verification method: " . $name);
            break;
    }
}

// --- 5. Send a Success Response ---

// Send a 200 OK response to let Trust Swiftly know you have successfully received the webhook.
http_response_code(200);
echo 'Webhook received successfully.';

?>
```

### Example Signature Verification (PHP)

```php
    public function verifyWebhook(Request $request)
    {

        $computed_signature = hash_hmac(
            'sha256', 
            $request->getContent(), 
            config('services.trustswiftly.signature_secret')
        );

        $received_signature = $_SERVER['HTTP_SIGNATURE'];

        if($computed_signature !== $received_signature) {
            \Log::info('received_signature wrong');
            return response('Tampered Request', 500);
        }

        $user = User::find($request->reference_id);

        if (! $user) {
            \Log::info('not found user');
            return response('Tampered Request', 500);
        }

        $requiredVerifications = [];
        foreach($request->verifications as $verification) {
            $requiredVerifications[$verification['id']] = $verification['status']['value'];
        }

        $user->required_verifications = $requiredVerifications;
        $user->save();

        return response(200);
    }
```

### Example Signature Verification (JS)

```javascript
// Import required modules
const express = require('express');
const crypto = require('crypto');

// --- Configuration ---

// It is a critical security practice to store your secret outside of your codebase.
// Use environment variables to load your secret key.
// Example: TRUST_SWIFTLY_SECRET=XXXX
const webhookSecret = process.env.TRUST_SWIFTLY_SECRET;
if (!webhookSecret) {
    // Fail fast if the secret is not configured
    console.error("FATAL ERROR: TRUST_SWIFTLY_SECRET environment variable not set.");
    process.exit(1);
}

const app = express();
const PORT = process.env.PORT || 3000;
const SIGNATURE_HEADER = 'Signature';

// --- Webhook Verification Middleware ---

// This custom middleware verifies the webhook signature *before* your route handler runs.
const verifyTrustSwiftlyWebhook = (req, res, next) => {
    // 1. Get the signature from the request header.
    const receivedSignature = req.get(SIGNATURE_HEADER);

    if (!receivedSignature) {
        console.warn('Webhook failed: Signature header missing.');
        return res.status(400).send('Signature header is required.');
    }

    // 2. Compute the expected signature.
    // The signature is an HMAC-SHA256 hash of the raw request body.
    const hmac = crypto.createHmac('sha256', webhookSecret);
    hmac.update(req.rawBody); // Use the raw body saved by the express.json middleware
    const computedSignature = hmac.digest('hex');

    // 3. Securely compare the signatures.
    // Use crypto.timingSafeEqual to prevent timing attacks. It requires Buffer inputs.
    const receivedSigBuffer = Buffer.from(receivedSignature, 'utf8');
    const computedSigBuffer = Buffer.from(computedSignature, 'utf8');
    
    if (receivedSigBuffer.length !== computedSigBuffer.length || !crypto.timingSafeEqual(receivedSigBuffer, computedSigBuffer)) {
        console.warn('Webhook failed: Invalid signature.');
        return res.status(403).send('Tampered Request: Invalid signature.');
    }

    // 4. If the signature is valid, proceed to the actual route handler.
    next();
};

// --- Express App Setup ---

// We need the raw request body to compute the signature. The `verify` function
// of the express.json middleware allows us to capture it as a Buffer.
app.use(express.json({
    verify: (req, res, buf) => {
        if (buf && buf.length) {
            req.rawBody = buf;
        }
    },
}));

// --- Webhook Route ---

// Define the route for receiving webhooks.
// Apply the verification middleware *before* your main handler.
app.post('/webhooks/trustswiftly', verifyTrustSwiftlyWebhook, (req, res) => {
    console.log('Webhook signature verified successfully!');

    // Now you can safely process the JSON payload.
    const webhookData = req.body;
    console.log(`Received event: ${webhookData.event}`);

    // TODO: Add your business logic here.
    // For example, update a user's status in your database based on the webhook event.
    // const { reference_id, verifications } = webhookData;
    // updateUserVerificationStatus(reference_id, verifications);

    res.status(200).json({ status: 'success', message: 'Webhook received' });
});

// --- Server Startup ---

app.listen(PORT, () => {
    console.log(`Server listening on port ${PORT}`);
    console.log('To test, send a POST request to http://localhost:3000/webhooks/trustswiftly');
});
```

### Python Example (using Flask)

This example uses the Flask web framework to create a simple endpoint for receiving the webhook. The standard hashlib and hmac libraries are used for signature verification.

```python
# File: trustswiftly_webhook_handler.py

import hmac
import hashlib
import os
import json
from flask import Flask, request, abort

app = Flask(__name__)

# It's best practice to load the webhook secret from an environment variable.
# NEVER hardcode secrets in your application.
TRUST_SWIFTLY_WEBHOOK_SECRET = os.environ.get('TRUST_SWIFTLY_WEBHOOK_SECRET')

if not TRUST_SWIFTLY_WEBHOOK_SECRET:
    raise ValueError("TRUST_SWIFTLY_WEBHOOK_SECRET environment variable not set.")


@app.route('/webhooks/trustswiftly', methods=['POST'])
def trust_swiftly_webhook():
    """
    Receives and securely verifies a webhook from Trust Swiftly.
    """
    # --- 1. Signature Verification ---
    # The signature is calculated on the raw, unmodified request body.
    # It is crucial to use the raw bytes (`request.data`) for the calculation.
    
    # Get the signature from the request headers.
    received_signature = request.headers.get('Signature')
    if not received_signature:
        print("Webhook failed: 'Signature' header not found.")
        abort(400, "Signature header is required.")

    # Get the raw request body as bytes.
    payload_bytes = request.data

    # Compute the expected signature using the shared secret.
    # The secret must be UTF-8 encoded bytes.
    computed_hash = hmac.new(
        TRUST_SWIFTLY_WEBHOOK_SECRET.encode('utf-8'),
        payload_bytes,
        hashlib.sha256
    )
    computed_signature = computed_hash.hexdigest()

    # Securely compare the received signature with the one we computed.
    # hmac.compare_digest is essential to prevent timing attacks.
    if not hmac.compare_digest(computed_signature, received_signature):
        print("Webhook failed: Signature mismatch.")
        # For debugging, you can print the signatures, but be careful in production.
        # print(f"  Computed: {computed_signature}")
        # print(f"  Received: {received_signature}")
        abort(403, "Tampered Request: Signature mismatch.")

    print("Signature verified successfully!")

    # --- 2. Process the Webhook Payload ---
    # Once the signature is verified, you can safely process the JSON data.
    try:
        webhook_data = json.loads(payload_bytes)
    except json.JSONDecodeError:
        print("Webhook failed: Invalid JSON payload.")
        abort(400, "Invalid JSON.")

    # TODO: Add your business logic here.
    # For example, you can use a queue to handle the event asynchronously.
    event_type = webhook_data.get('event_type') or webhook_data.get('event') # Handle new and old formats
    print(f"Received event '{event_type}' for Trust ID: {webhook_data.get('trust_id')}")

    # --- 3. Acknowledge Receipt ---
    # Respond with a 200 OK to let Trust Swiftly know you've received the webhook.
    # If you don't respond with 2xx, Trust Swiftly will retry sending the webhook.
    return "Webhook received and verified.", 200


if __name__ == '__main__':
    # This is a basic development server. For production, use a WSGI server like Gunicorn or uWSGI.
    #
    # To run this example:
    # 1. Install Flask: pip install Flask
    # 2. Set the environment variable: export TRUST_SWIFTLY_WEBHOOK_SECRET='your_actual_secret'
    # 3. Run the script: python trustswiftly_webhook_handler.py
    #
    # --- How to Test with cURL ---
    # To correctly test this endpoint, your curl command must replicate the exact
    # payload your server sends, including the escaped forward slash `\/`.
    #
    # secret='your_actual_secret'
    #
    # # Note the escaped slash `\/` in the JSON string. This is crucial.
    # payload='{"event":"user.status.changed","name":"Phone \/ SMS"}'
    #
    # # Generate the signature based on this exact payload
    # sig=$(echo -n "$payload" | openssl dgst -sha256 -hmac "$secret" | cut -d ' ' -f2)
    #
    # # Send the request
    # curl -X POST http://127.0.0.1:5000/webhooks/trustswiftly \
    #   -H "Content-Type: application/json" \
    #   -H "Signature: $sig" \
    #   -d "$payload"
    #
    app.run(port=5000, debug=True)

```

### Laravel / PHP Example

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Log;

class TrustSwiftlyWebhookController extends Controller
{
    /**
     * Handle a Trust Swiftly webhook request.
     *
     * @param \Illuminate\Http\Request $request
     * @return \Illuminate\Http\Response
     */
    public function handle(Request $request)
    {
        // 1. Get the signature from the request headers.
        // The header key is case-insensitive, but 'Signature' is standard.
        $receivedSignature = $request->header('Signature');

        if (!$receivedSignature) {
            Log::warning('Trust Swiftly Webhook: Signature header not found.');
            return response('Signature header is required.', 400);
        }

        // 2. Get the secret key from your configuration.
        // Ensure this key exists in config/services.php
        $secret = config('services.trust.signature_secret');
        if (!$secret) {
            Log::error('Trust Swiftly Webhook: Signature secret is not configured.');
            return response('Server configuration error.', 500);
        }

        // 3. Compute the expected signature.
        // It is crucial to use $request->getContent() to get the raw, unmodified request body.
        $payload = $request->getContent();
        $computedSignature = hash_hmac('sha256', $payload, $secret);

        // 4. Compare the signatures securely.
        // Use hash_equals() for a constant-time comparison to prevent timing attacks.
        if (!hash_equals($computedSignature, $receivedSignature)) {
            Log::warning('Trust Swiftly Webhook: Signature mismatch.', [
                'computed' => $computedSignature,
                'received' => $receivedSignature,
            ]);
            return response('Tampered Request: Invalid signature.', 403);
        }

        // If the signature is valid, process the payload
        Log::info('Trust Swiftly Webhook: Signature verified successfully!');
        $webhookData = json_decode($payload, true);

        // TODO: Add your business logic here.
        // For example, find a user by `reference_id` and update their verification status.
        // $event = $webhookData['event'];
        // $referenceId = $webhookData['reference_id'];
        
        return response('Webhook received.', 200);
    }
}
```

\


