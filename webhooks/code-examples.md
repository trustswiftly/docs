# Webhook Code Examples

### Example Payload

```javascript
{
  "id": "237d6330-f8e0-410b-b927-dd7b07bf99ec",
  "ip": null,
  "event": "verification.pending",
  "trust_id": 1,
  "created_at": "2020-09-11T01:33:51.000000Z",
  "ip_country": null,
  "user_status": "Active",
  "reference_id": null,
  "last_activity": "2020-11-10 12:27:16",
  "verifications": [
    {
      "id": 1,
      "name": "Email",
      "status": {
        "value": 0,
        "friendly": "Pending"
      }
    },
    {
      "id": 2,
      "name": "Phone / SMS",
      "status": {
        "value": 0,
        "friendly": "Pending"
      }
    },
    {
      "id": 3,
      "name": "Document / ID",
      "status": {
        "value": 0,
        "friendly": "Pending"
      }
    }
  ]
}
```

### Example Handling

```php
$payload = @file_get_contents('php://input');
$event = null;
$json = json_decode($payload);

//first lets validate the request!
$computed_signature = hash_hmac('sha256', file_get_contents("php://input"), $configuredSigningSecret);
$received_signature = $_SERVER['HTTP_SIGNATURE'];

if($computed_signature !== $received_signature) {
    http_response_code(500);
    die('Tampered Request');
}

foreach($json->verifications as $verification) {
    switch($verification->name) {
        case "Email":

        break;
        case "Phone / SMS":

        break;
        default:
            echo 'We received a different verification method! - '.$verification->verification;
    }
}

http_response_code(200);
```

### Verify Signature

```php
    public function verifyWebhook(Request $request)
    {

        $computed_signature = hash_hmac(
            'sha256', 
            $request->getContent(), 
            config('services.trust.key')
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

