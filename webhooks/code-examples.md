# Webhook Code Examples

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

