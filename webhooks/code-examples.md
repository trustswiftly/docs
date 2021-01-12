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
      "status": "Pending",
      "verification": "Email"
    },
    {
      "status": "Pending",
      "verification": "Phone / SMS"
    },
    {
      "status": "Pending",
      "verification": "Document / ID"
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
$received_signature = $_SERVER['HTTP_Signature'];

if($computed_signature !== $received_signature) {
    http_response_code(500);
    die('Tampered Request');
}

foreach($json->verifications as $verification) {
    switch($verification->verification) {
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

