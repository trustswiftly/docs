# Webhook Code Examples

To ensure the integrity and authenticity of the webhooks sent from Trust Swiftly, we sign every request sent to your endpoint. By verifying this signature, you can confirm that the webhook was sent by Trust Swiftly and that its payload has not been tampered with during transmission.

The signature is an **HMAC-SHA256 hash**, generated using your unique webhook signing secret and the raw request body. This signature is passed in the **`Signature` HTTP header** with each request.

Below are code examples demonstrating how to properly verify the webhook signature in several common languages and frameworks. It is crucial to use a secure, constant-time comparison method to prevent timing attacks.

* PHP (Procedural)
* PHP (Laravel)
* JavaScript (Express.js)
* Python (Flask)

***

### Example Payload (`verification.completed`)

The new webhook format encapsulates the main payload within `data` and `relationships` objects. All custom business logic should now access data through these keys.

```json
{
  "id": "4e057b68-0d5f-40ad-b84a-a4d878b738fd",
  "type": "verification.completed",
  "subject": "verification",
  "spec_version": "2025-10-08",
  "occurred_at": "2025-10-08T23:55:09+00:00",
  "resource_id": 1,
  "relationships": {
    "user_id": 172,
    "user_uuid": "0199c63f-a1d4-7400-bc22-8cdfaad82084"
  },
  "data": {
    "verification_id": 1,
    "verification_name": "Email verification",
    "email": "testwebhook@trustswiftly.com",
    "user_status": "Active",
    "order_id": null,
    "ip": "172.19.0.7",
    "ip_country": "US",
    "reference_id": "5122",
    "last_activity": "2025-10-08T23:54:50+00:00",
    "verifications": [
      {
        "id": 1,
        "name": "Email",
        "status": {
          "value": 2,
          "friendly": "Complete"
        },
        "attributes": {
          "email": "testwebhook@trustswiftly.com",
          "paypal_email": "testwebhook@trustswiftly.com",
          "paypal_email_verified": 0
        },
        "start_time": "2025-10-08 23:54:43",
        "completion_time": "2025-10-08 23:55(0 h 0 m 26 s)",
        "completed_at": "2025-10-08 23:55"
      },
      {
        "id": 3,
        "name": "Document / ID",
        "status": {
          "value": 0,
          "friendly": "Assigned"
        },
        "attributes": {
          "verify_documents": [],
          "workflow": "ID + Selfie"
        }
      }
    ]
  }
}
```

***

### PHP (Procedural) Example

```php
<?php

/**
 * Procedural PHP example for verifying Trust Swiftly Webhooks.
 */

// --- 1. Configuration ---
// It is a critical security practice to store your secret outside of your codebase.
// $webhookSecret = getenv('TRUST_SWIFTLY_SECRET');
$webhookSecret = 'XXXX'; // Replace with your actual webhook signing secret.

// --- 2. Get Request Data ---
$payload = file_get_contents('php://input');
if ($payload === false || empty($payload)) {
    http_response_code(400);
    exit('Error: Could not read request body.');
}

if (!isset($_SERVER['HTTP_SIGNATURE'])) {
    http_response_code(400);
    exit('Error: Signature header is missing.');
}
$receivedSignature = $_SERVER['HTTP_SIGNATURE'];


// --- 3. Verify the Signature ---
$computedSignature = hash_hmac('sha256', $payload, $webhookSecret);

// Use hash_equals() for a secure, constant-time comparison to prevent timing attacks.
if (!hash_equals($computedSignature, $receivedSignature)) {
    http_response_code(403);
    exit('Tampered Request: Invalid signature.');
}


// --- 4. Process the Payload ---
$webhookData = json_decode($payload, true);

if (json_last_error() !== JSON_ERROR_NONE) {
    http_response_code(400);
    exit('Error: Invalid JSON payload.');
}

// **UPDATED FOR NEW FORMAT**: Access data from the 'data' and 'relationships' objects.
$data = $webhookData['data'] ?? [];
$relationships = $webhookData['relationships'] ?? [];
$eventType = $webhookData['type'] ?? 'unknown';

$referenceId = $data['reference_id'] ?? null; // Your internal user ID
$verifications = $data['verifications'] ?? [];
$trustSwiftlyUserId = $relationships['user_id'] ?? null;

// TODO: Add your business logic here.
// Find the user in your system using $referenceId.
// error_log("Processing event '{$eventType}' for reference ID: {$referenceId}");

foreach ($verifications as $verification) {
    $name = $verification['name'] ?? 'Unknown';
    $status = $verification['status']['friendly'] ?? 'unknown';

    // Example: Log the result for the specific user
    // error_log("Verification for user {$referenceId}: {$name} - Status: {$status}");
}

// --- 5. Send a Success Response ---
// Acknowledge receipt to prevent retries from Trust Swiftly.
http_response_code(200);
echo 'Webhook received successfully.';

?>
```

***

### PHP (Laravel) Example

```php
<?php

namespace App\Http\Controllers;

use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Log;

class TrustSwiftlyWebhookController extends Controller
{
    /**
     * Handle a Trust Swiftly webhook request.
     */
    public function handle(Request $request)
    {
        // 1. Get the signature from the headers.
        $receivedSignature = $request->header('Signature');
        if (!$receivedSignature) {
            Log::warning('Trust Swiftly Webhook: Signature header not found.');
            return response('Signature header is required.', 400);
        }

        // 2. Get the secret key from your configuration (e.g., config/services.php).
        $secret = config('services.trustswiftly.signature_secret');
        if (!$secret) {
            Log::error('Trust Swiftly Webhook: Signature secret is not configured.');
            return response('Server configuration error.', 500);
        }

        // 3. Compute the expected signature from the raw request body.
        $payload = $request->getContent();
        $computedSignature = hash_hmac('sha256', $payload, $secret);

        // 4. Securely compare signatures to prevent timing attacks.
        if (!hash_equals($computedSignature, $receivedSignature)) {
            Log::warning('Trust Swiftly Webhook: Signature mismatch.');
            return response('Tampered Request: Invalid signature.', 403);
        }

        // 5. Process the payload now that the signature is verified.
        Log::info('Trust Swiftly Webhook: Signature verified successfully!');
        $webhookData = json_decode($payload, true);
        
        // **UPDATED FOR NEW FORMAT**: Access data from the 'data' and 'relationships' objects.
        $data = $webhookData['data'] ?? [];
        
        $referenceId = $data['reference_id'] ?? null;
        if (!$referenceId) {
            Log::info('Trust Swiftly Webhook: reference_id not found in payload.');
            return response('Webhook processed, no reference_id.', 200);
        }
        
        $user = User::find($referenceId);
        if (!$user) {
            Log::info("Trust Swiftly Webhook: User not found for reference_id: {$referenceId}.");
            return response('User not found.', 200); // Respond 200 to acknowledge.
        }

        // Example logic: Save the verification data to a user meta field.
        $verifications = $data['verifications'] ?? [];
        $user->trustswiftly_verifications = $verifications;
        $user->save();

        Log::info("Trust Swiftly Webhook: Updated verifications for User ID {$user->id}.");
        
        return response('Webhook received.', 200);
    }
}
```

***

### JavaScript (Express.js) Example

```javascript
// Import required modules
const express = require('express');
const crypto = require('crypto');

// --- Configuration ---
// It is a critical security practice to store your secret outside of your codebase.
// Use environment variables: export TRUST_SWIFTLY_SECRET=your_secret_key
const webhookSecret = process.env.TRUST_SWIFTLY_SECRET;
if (!webhookSecret) {
    console.error("FATAL ERROR: TRUST_SWIFTLY_SECRET environment variable not set.");
    process.exit(1);
}

const app = express();
const PORT = process.env.PORT || 3000;

// --- Express App Setup ---
// Capture the raw request body as a Buffer, which is required for signature verification.
app.use(express.json({
    verify: (req, res, buf) => {
        req.rawBody = buf;
    },
}));

// --- Webhook Verification Middleware ---
// Verifies the signature *before* your route handler runs.
const verifyTrustSwiftlyWebhook = (req, res, next) => {
    const receivedSignature = req.get('Signature');
    if (!receivedSignature) {
        console.warn('Webhook failed: Signature header missing.');
        return res.status(400).send('Signature header is required.');
    }

    const hmac = crypto.createHmac('sha256', webhookSecret);
    // Use the raw body buffer saved by the express.json middleware
    hmac.update(req.rawBody); 
    const computedSignature = hmac.digest('hex');

    // Use crypto.timingSafeEqual for a secure, constant-time comparison.
    try {
        const receivedSigBuffer = Buffer.from(receivedSignature, 'utf8');
        const computedSigBuffer = Buffer.from(computedSignature, 'utf8');
        if (!crypto.timingSafeEqual(receivedSigBuffer, computedSigBuffer)) {
             console.warn('Webhook failed: Invalid signature.');
             return res.status(403).send('Tampered Request: Invalid signature.');
        }
    } catch (error) {
        console.warn('Webhook failed: Error during signature comparison.');
        return res.status(403).send('Tampered Request: Invalid signature.');
    }

    // Signature is valid, proceed to the route handler.
    next();
};


// --- Webhook Route ---
app.post('/webhooks/trustswiftly', verifyTrustSwiftlyWebhook, (req, res) => {
    console.log('Webhook signature verified successfully!');

    // **UPDATED FOR NEW FORMAT**: Access data from the 'data' and 'relationships' objects.
    const { type, data, relationships } = req.body;
    console.log(`Received event: ${type}`);

    // Your business logic goes here.
    if (data && relationships) {
        const { reference_id, verifications } = data;
        const { user_id } = relationships;
        
        console.log(`Processing data for your user ID (reference_id): ${reference_id}`);
        // Example: updateUserVerificationStatus(reference_id, verifications);
    }
    
    // Acknowledge receipt with a 200 OK response.
    res.status(200).json({ status: 'success', message: 'Webhook received' });
});

app.listen(PORT, () => console.log(`Server listening on port ${PORT}`));
```

***

### Python (Flask) Example

```python
import hmac
import hashlib
import os
import json
from flask import Flask, request, abort

app =Flask(__name__)

# --- Configuration ---
# Load the webhook secret from an environment variable for security.
# NEVER hardcode secrets.
# export TRUST_SWIFTLY_WEBHOOK_SECRET='your_secret'
TRUST_SWIFTLY_WEBHOOK_SECRET = os.environ.get('TRUST_SWIFTLY_WEBHOOK_SECRET')
if not TRUST_SWIFTLY_WEBHOOK_SECRET:
    raise ValueError("TRUST_SWIFTLY_WEBHOOK_SECRET environment variable not set.")


@app.route('/webhooks/trustswiftly', methods=['POST'])
def trust_swiftly_webhook():
    """Receives and securely verifies a webhook from Trust Swiftly."""
    
    # --- 1. Signature Verification ---
    received_signature = request.headers.get('Signature')
    if not received_signature:
        print("Webhook failed: 'Signature' header not found.")
        abort(400, "Signature header is required.")

    # Get the raw request body as bytes (`request.data`).
    payload_bytes = request.data

    # Compute the expected signature using the shared secret.
    # Note: The secret must be encoded to bytes before use in hmac.new.
    computed_hash = hmac.new(
        TRUST_SWIFTLY_WEBHOOK_SECRET.encode('utf-8'),
        payload_bytes,
        hashlib.sha256
    )
    computed_signature = computed_hash.hexdigest()

    # Use hmac.compare_digest for secure, constant-time comparison to prevent timing attacks.
    if not hmac.compare_digest(computed_signature, received_signature):
        print("Webhook failed: Signature mismatch.")
        abort(403, "Tampered Request: Signature mismatch.")

    print("Signature verified successfully!")

    # --- 2. Process the Webhook Payload ---
    try:
        webhook_data = json.loads(payload_bytes)
    except json.JSONDecodeError:
        print("Webhook failed: Invalid JSON payload.")
        abort(400, "Invalid JSON.")
    
    # **UPDATED FOR NEW FORMAT**: Access data from nested objects.
    event_type = webhook_data.get('type', 'unknown')
    data = webhook_data.get('data', {})
    relationships = webhook_data.get('relationships', {})

    reference_id = data.get('reference_id')
    user_uuid = relationships.get('user_uuid')

    # TODO: Add your business logic here.
    print(f"Received event '{event_type}' for user UUID: {user_uuid} (Reference ID: {reference_id})")

    # --- 3. Acknowledge Receipt ---
    # Respond with 200 OK to prevent webhook retries.
    return "Webhook received and verified.", 200


if __name__ == '__main__':
    # For development only. Use a production WSGI server (like Gunicorn) in production.
    app.run(port=5000, debug=True)
```
