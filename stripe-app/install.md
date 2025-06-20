---
description: >-
  The below instructions can be used for demo purposes and for live transactions
  you can consult with our team for optimal setup with Radar rules.
---

# Install and Demo Guide

**Stripe App Integration Guide**

Automate your payment review process, reduce manual work, and fight fraud by integrating Trust Swiftly directly with your Stripe account. This guide will walk you through setting up the Trust Swiftly Stripe App, configuring Stripe Radar rules, and testing the end-to-end workflow.

When a payment is sent to your review queue in Stripe, Trust Swiftly automatically triggers a verification process for the customer. If they pass, the review is approved automatically.

**Prerequisites**

Before you begin, ensure you have the following:

* **A Trust Swiftly Account:** Sign up at [trustswiftly.com](https://trustswiftly.com).
  * **Free Radar Consultation:** To help you maximize revenue, we offer a free initial consultation on optimizing your Stripe Radar rules for new customers with a deposit of $300 or more.
* **A Stripe Account** with administrator access.

***

#### **Part 1: Installation and Connection**

First, you'll log in to Trust Swiftly and install the app from the Stripe Marketplace.

1. **Sign in to Trust Swiftly**
   * Navigate to your tenant URL: `https://[COMPANY].trustswiftly.com/login` (replace `[COMPANY]` with your unique name).
   * Enter your admin username and password.
2. **Install the Trust Swiftly Stripe App**
   * Go to the Stripe App connection page in your settings: `https://[COMPANY].trustswiftly.com/settings/stripe_app`
   * You will be guided to find the **Trust Swiftly** app in the Stripe Marketplace (under the "Compliance & Identity" category).
   * During the installation process in Stripe, you will be asked to provide your domain. Enter your full Trust Swiftly tenant URL: `https://[COMPANY].trustswiftly.com`.
3. **Verify the Installation**
   * After the app is installed, return to the Trust Swiftly settings page.
   * The status should update automatically. If it doesn't, click the **Verify Install** button.

> **Important Note on Test Mode:** If you are operating in Stripe's test mode, you must enable "Test mode" on the Trust Swiftly Stripe App connection page to ensure transactions are handled correctly.

***

#### **Part 2: Configuration in Trust Swiftly**

Next, configure how the app behaves within your Trust Swiftly dashboard.

1. Navigate back to the **Connect Stripe App** page (`.../settings/stripe_app`).
2. **Default Verification Template:** Select a verification template that will be sent to customers whose payments are sent to review.
3. **Approve Reviews Automatically:** Enable this toggle so that when a user successfully passes verification, the corresponding review in Stripe is automatically approved.
4. **User Email Notifications:** Enable this to ensure users receive an email with the link to complete their verification.
5. Click **Update Settings** to save.

***

#### **Part 3: Configure Stripe Radar Rules**

For the integration to work, you must tell Stripe which payments to send to the review queue.

1. Navigate to your **Stripe Radar rules**: [dashboard.stripe.com/settings/radar/rules](https://dashboard.stripe.com/settings/radar/rules).
2. Scroll down to the **"When should a payment be placed in review?"** section.
3. Click **+ Add rule**.
4. Create a condition to trigger a review. For example, you can create a rule for high-risk payments:   `Request a review if :risk_score: > 50 and :amount_in_usd: > 500.00`
5. Click **Test rule** to see how it behaves, then click **Save** to enable it.

> **Need help with Radar?** Setting up effective Radar rules is key to maximizing revenue and minimizing fraud. [**Contact our team**](https://trustswiftly.com/contact) for help with a custom-tailored optimization service.

***

#### **Part 4: Demo and Test the Workflow**

Follow these steps to perform an end-to-end test and see the integration in action.

1. **Create a Test Payment**
   * In your Stripe dashboard, go to **Payment Links** and create a new link.
   * Add a new product with a price that will be triggered by the Radar rule you just created (e.g., $501).
   * Under the advanced options, ensure you **require customers to provide a phone number**.
   * Click **Create link**.
2. **Simulate a Customer Purchase**
   * Copy the payment link and open it in a **new incognito browser window**. This prevents session conflicts.
   * Fill out the payment details using a test email and credit card, then click **Pay**.
3. **Verify the Payment is in Review**
   * Navigate to your **Radar for Reviews** queue in Stripe: [dashboard.stripe.com/radar/reviews](https://dashboard.stripe.com/radar/reviews).
   * You should see the payment you just made listed here.
4. **Complete the Verification (as the customer)**
   * Check the inbox for the email address you used in the test payment.
   * Open the email from Trust Swiftly and click the **Verify** button.
   * You will be taken to the verification flow. Complete the steps (e.g., enter an SMS code).
5. **Confirm Automatic Approval**
   * Return to your Radar review queue in Stripe.
   * Once the verification is passed, the payment should automatically disappear from the review list, indicating it has been approved.
