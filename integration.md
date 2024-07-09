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

![Created keys to save](<.gitbook/assets/image (24).png>)

##
