---
description: >-
  This integration guide is for setting up our embedded verification option.
  Complete the prerequisites before integrating the flow.
---

# Integration

## **Prerequisites**

### Step 1

Following the account creation, create your branded verification site for verifying your users. Your users will be verified on this URL for hosted integrations.

**Parameter to Note: `baseUrl`**

![](<.gitbook/assets/image (20).png>)

### Step 2

Create a template(s) for required verification(s) to assign to your users. You can create multiple templates and then use those templates as conditions to invoke multiple verification combinations to your users when they are created or trigger a risk action.

**Parameter to Note: `template_id`**

![Click Add Template](<.gitbook/assets/image (21).png>)

![Input the name and enable each verification assigned to the template](<.gitbook/assets/image (22).png>)

### Step **3** <a href="#step-2" id="step-2"></a>

Generate your API keys by going to the Settings -> Developer, click on the create key to generate your key.

![Click Create API Key](<.gitbook/assets/image (23).png>)

The keys are only visible once so please copy and save the keys.

**KEY (`api_key`) :** This key will be used for API calls which are done through the server of your applications. For example: [Create User API](users.md#create-user)

**SECRET (`secret`):** This secret will be used for generating signature for using our embed integration on your application. (See the signature generation ahead)

**Embed Key (`embedKey`):** This key should be used in the embed integration on your application as well as part of generating the signature.

![Created keys to save](<.gitbook/assets/image (24).png>)

## Integration Flow (Embed)

### Step **1** <a href="#step-2" id="step-2"></a>

The flow starts with creating a user through the [Create User API](users.md#create-user), which will return the `user_id`for the user.

Send the `template_id`in the create user request to assign the verifications required for any new user.

_Optionally_ include a `reference_id` to link created users in Trust Swiftly to your original application.

```
https://{Your base URL}/api/users

{
  "status": "success",
  "id": 69,
  "user_id": "3639",
  "magic_link": "https:\/\/test.trustswiftly.com\\/security-verify?expires=1625603631&key=16RWTtJRKTwjFIQCGWsdarWkW4Qq2DdvfUQhdzvug3AVwWu5mbZht&signature=768898ec51b20a623ba813969215fe9c113c3a7232204c0046265b3c6"
}
```

**Parameter to Note:** `user_id`

Store the user id for all the further communications with the API and for rendering the embed flow.

### Step 2 <a href="#step-2" id="step-2"></a>

Generating signature for API calls in the embed integration.

For generating signature we use a SHA256 hash algorithm, the PHP implementation example is below:

```php
$embedKey = 'xxxxxxx';
$secret = 'xxxxxxxxx';
$user_id = 12345;
$timestamp = time();
$payloadString = $embedKey . $user_id . $timestamp;
$hash = hash_hmac('sha256', $payloadString, $secret);
$signature = 't=' . $timestamp . ',v2=' . $hash;
$apisecret = '0761ac60dadd3c0a8fe636c0b7cba4ef90c277f77a5b4b27add7cd3f572eec58';
$embedKey = "32daa045246eaa06716ff7b4c34bbd6528df6968";
$timestamp = time();
$payloadString = $embedKey . $user_id . $timestamp;
$hash = hash_hmac('sha256', $payloadString, $apisecret);
$signature = 't=' . $timestamp . ',v2=' . $hash;
```

This signature is required for the next step to display the embed integration.

### Step 3 <a href="#step-2" id="step-2"></a>

There are 3 methods to display the embedded integration.

1. Embed within your page
2. Embed with a Bootstrap modal and our button
3. (Optional) Use the embed in page but only possible if you have a single type of verify.

The prerequisites for using the embed integration is to have jQuery 3.6 or up and Bootstrap 5 in your application, the CDN links are given as below.

```markup
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.0.2/js/bootstrap.min.js"> </script>
<script src="https://cdn.trustswiftly.com/assets/js/trustverifyv2.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/5.0.2/css/bootstrap.min.css" crossorigin="anonymous" />
```

Next you need to place a div where you require display of the contents.

```markup
<div id="trustVerify" class="bg-light p-5 rounded"> </div>
```

**Method 1** Use the embed integration in your page as embedded content.

```javascript
trustVerify.configs = {
    embedKey: '{ embedKey }',
    signature: '{ signature }',
    baseUrl: '{baseUrl}',
    type: 'page',
    verifyDivId: "trustVerify",
    userId: { user_id }
};
trustVerify.load();
```

This will generate the verify content in the HTML Dom element/div element with the id `trustVerify`

![](<.gitbook/assets/image (25).png>)

**Method 2** Use the embed integration modal in your page with the Trust Swiftly button/modal

```javascript
trustVerify.configs = {
    embedKey: '{ embedKey }',
    signature: '{ signature }',
    baseUrl: '{baseUrl}',
    type: 'modal',
    verifyDivId: "trustVerify",
    userId: { user_id }
};
trustVerify.load();
```

This will generate the Trust Swiftly verify button which would open the Bootstrap modal within the given div element.

![Example Button](<.gitbook/assets/image (26).png>)

![](<.gitbook/assets/image (27).png>)

**Method 3** Use the embed integration modal in your page to to directly show the specific verification. This is useful if your verification template only has one verification.

```javascript
trustVerify.configs = {
    embedKey: '{ embedKey }',
    signature: '{ signature }',
    baseUrl: '{baseUrl}',
    type: 'page',
    verifyCall: 'single', //options (single,multi)
    verifyMethod: 'email', //options(email,phone,document,voice,video..) only works with single call
    verifyDivId: "trustVerify",
    userId: { user_id }
};

trustVerify.loadSingle();
```

This will generate the verification in the same page similar to the 1st method but it will directly load the specific verification.

![Direct display of verification](<.gitbook/assets/image (28).png>)

### Step 4 <a href="#step-2" id="step-2"></a>

The completion calls and updating certain verifications for your user can be monitored through callbacks and webhooks. We recommend implementing two methods to ensure changes are tracked properly.

There are 3 ways to know if the user has completed a certain verification which are as mentioned below:

1. Using our JS completion functions

```javascript
onComplete: function(data) {
    alert('Verification Complete' + data.value)
}

//Or 

onStateChange: function(data) {
    if (data.method == "DOCUMENT") {
        if (data.state == "Successful") {
            alert('Verification Complete')
        }
    }
}
```

2\. Using our [webhook implementation guide](webhooks/handling-webhooks.md)

3\. Using the [Get User API call](users.md#get-user)
