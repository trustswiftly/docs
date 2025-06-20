# Prefill User Creation

**Prefilling User Information for Faster Manual Creation**

Streamline the manual creation of user profiles by pre-filling their information using URL parameters. This feature is ideal for situations where an administrator is creating a user account and has the user's data readily available. By passing the information directly in the URL, you can minimize manual data entry and reduce the chance of errors.

**How It Works**

To prefill the new user form, construct a URL that points to the `/user/quick_create` endpoint and append the user's data as query parameters. When an administrator clicks this link, they will be taken to the user creation page with all the specified fields already filled out. They can then review the details and finalize the account creation.

The base URL for this action is:`https://{your_subdomain}.trustswiftly.com/user/quick_create`

**Available Parameters**

You can use the following optional parameters to pre-populate the corresponding fields on the user creation form:

* `first_name`: The user's first name.
* `last_name`: The user's last name.
* `email`: The user's email address.
* `phone`: The user's phone number (URL-encoded).
* `template_id`: The ID of a specific verification template to assign to the user upon creation.
* `email_notify`: Set to `1` to enable email notifications for the user.
* `sms_notify`: Set to `1` to enable SMS notifications for the user.

All parameters are optional. You only need to include the ones you wish to prefill.

**Example Usage**

Imagine you want to create a new user named John Smith, assign a specific verification template, and enable all notifications. You would construct the following URL:

```
https://demo1.trustswiftly.com/user/quick_create?first_name=John&last_name=Smith&email=jsmith@example.com&phone=%2B13125551234&template_id=tmpl_MQ&email_notify=1&sms_notify=1
```

When an administrator accesses this URL, the user creation page will load with all of John's information pre-filled and the correct template selected. The administrator simply needs to review the details and click the **"Create"** button to complete the process.

This method allows for quick and accurate user setup, making it a powerful tool for administrative workflows.

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>
