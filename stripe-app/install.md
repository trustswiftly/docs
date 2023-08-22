---
description: >-
  The below instructions can be used for demo purposes and for live transactions
  you can consult with our team for optimal setup with Radar rules.
---

# Install and Demo Guide

`Note: If using test mode/ sandbox mode please enable the mode into the Stripe connect page`

* [ ] **Prerequisite**: [Create a Trust Swiftly account ](https://app.trustswiftly.com/create?ref=partner)(Deposit over $300 for a free initial consultation on your Stripe Rules. We help you optimize your rules for more revenue.)

**Sign in to your Trust Swiftly tenant**

1. Navigate to [https://\[COMPANY\].trustswiftly.com/login](https://stripetest.trustswiftly.com/login) (Replace \[company] with your specific tenant)
2. Enter in the your account username and password
3. Click Log In\


![](https://lh5.googleusercontent.com/x8tAyPzkWktteKO368-Pmduxw4FZzWqGCkQrsC6LuLxNrVMTWge\_7Q\_ZGkFDsfLx0cI3F6v0Ak3XDGb7Q1CnjQslcTd2DVi9OeN1F4AWGQcucqSoQHfbYlfGhWxHoLGXxjvGAionY1hT2fUtrdqspRg)

**Install the Trust Swiftly Stripe App**

1. Navigate to the **Connect Stripe App** page. [https://](https://stripetest.trustswiftly.com/settings/stripe\_app)[\[COMPANY\]](https://stripetest.trustswiftly.com/login)[.trustswiftly.com/settings/stripe\_app](https://stripetest.trustswiftly.com/settings/stripe\_app)&#x20;
2. Follow the instructions to install the app by going to Stripe's Marketplace and finding the Trust Swiftly app in the compliance category.&#x20;
3. Copy and paste your domain into the settings [https://](https://stripetest.trustswiftly.com/)[\[COMPANY\]](https://stripetest.trustswiftly.com/login)[.trustswiftly.com](https://stripetest.trustswiftly.com/)
4. After the app is installed on your Stripe account click the verify install button if not automatically updated.\


![](https://lh3.googleusercontent.com/cBeU6ThMHqIfR\_ydAxbdTJ0DVoUekYrjWSnjjeHIq-uS\_UXp2n1g7gZGr75jKDD1EutkXZ3Xsr-lbnQrG\_tUJ8BBWb5tDQGNNetjcyQANDq1At21XpyeXsPqUIwpz3bvTOnaf6-fN9WkRloLFpyyyDE)

**Configure Stripe App Options**

1. Select a value for the Default Verification Template field for one setup in your account.
2. Enable the toggles for Approve Reviews Automatically and User Email Notifications
3. Click Update Settings to save.

![](https://lh3.googleusercontent.com/j9KcvR8c5m\_YIoVRWiH4uPs6JJS\_aXZg9n3GX6BiYMHzYUIiTrvTKwBtGqT-mSAGrYOnD93RBCwSmxv6ycMaQIzz4RDjz6jR0nZo4b2AZWYHKkQ7IgSKXN01nlxYAEAbPvQMzXuyG\_NJODBHu358i7Q)\


**Configure Stripe Radar to send payments to review**

1. Navigate to Stripe Radar rules. [https://dashboard.stripe.com/settings/radar/rules](https://dashboard.stripe.com/settings/radar/rules)
2. Scroll to the Review rules section and click the Add Rule button
3. Create a review rule to send any payment over $500 and risk\_score > 50 to review or create your own logic [following our tips](https://trustswiftly.com/blog/optimal-fraud-prevention-with-stripe-radar-rules/) when you are ready for production. `Need help setting up Stripe Radar?` [`Contact us`](https://trustswiftly.com/contact-us/)`for a Stripe Radar rules optimization service.`&#x20;
4. Click Test rule and save the rule.
5. Any future payments that are sent to review will automatically be verified by Trust Swiftly.\


![](https://lh6.googleusercontent.com/Hq6dxtSjLmlSIOPfXAA3P3DmXmAQGXCQvHbFWYg-yHbzpSB4QV3P2nWSC4gWYlgf9mYchgGBJjviEuJF5vZEdd1PbAqKG52W4P2yzNvoottmyeAI0QjVRQJU6\_e6ankcij6PtFoFEPipMrFjhmzc2Kg)\


### Demo Steps

**Create a test payment that is put in review**

1. Navigate to payment links in Stripe and create a test payment link [https://dashboard.stripe.com/payment-links/create](https://dashboard.stripe.com/payment-links/create)
2. Add a new product called Test Review with a value that will be triggered by your rule. For demo purposes you may need to create a unique rule based on email.&#x20;
3. Check the option for Require customers to provide a phone number
4. Click Create Link button in top right corner.&#x20;
5. Copy the payment link and open a new incognito browser window so your other Trust Swiftly session is not impacted with the test.&#x20;
6. Populate the payment fields with phone number, email address, and credit card details and click the Pay button.&#x20;
7. Now navigate to the Radar review queue to verify the payment was placed in the list [https://dashboard.stripe.com/radar/reviews](https://dashboard.stripe.com/radar/reviews) \


![](https://lh3.googleusercontent.com/Iv\_raYjCZfOgWI0XIvo6jPljR1FnvIRZ9SZmXzfNOjX2pWXhRhOXQL9v\_jafYDchaqRVfWdrJbeoYBVcDJ3kTFmo1DnaAbEfapdPu7PtVA-gLqla48Z8ccpCMCSBJmdHuEPM9FUNLHgOeMqBx11GaQ8)



**Complete the Trust Swiftly verification**

1. Check the email you used for the test payment and click the Verify button to start.
2. Next on the dashboard click Verify now
3. Next click the Send SMS/Call Code.
4. Enter the code to complete the verification.&#x20;
5. Finally navigate to the Radar review queue to see if the payment was approved. If it was approved it should no longer be viewable here: [https://dashboard.stripe.com/radar/reviews](https://dashboard.stripe.com/radar/reviews)&#x20;

![](https://lh4.googleusercontent.com/cJQOwgyAUuFGLDRWxWpu6nqBny8LAP4Mayyu0QK-Fmu8z5GtNrLnQMeZwf5zQFFLhJHDrxKjhOLowuxX-jMZ581jYjvVD2oEzdxVj5vUrJSIm9Dj9QkNpjGxeFEsGYGrGxPWL5jQ8CNwSlgj32UJjYw)![](../.gitbook/assets/image.png)
