# Quick Create: Prefill User Data

**Streamline manual user creation by pre-filling profile information via URL.**

This feature is designed for administrators who need to manually create users but want to skip the repetitive data entry. By passing user data directly into the URL, you can load the User Creation page with fields already completed, reducing errors and saving clicks.

#### How It Works

To prefill the form, construct a URL pointing to the `/admin/user/quick_create` endpoint and append the user's data as query parameters.

When an administrator clicks this link, they are taken to the creation page with the data populated. They simply need to review and click **Create**.

**Base URL:** `https://{your_subdomain}.trustswiftly.com/admin/user/quick_create`

#### Available Parameters

Append these optional parameters to the Base URL to pre-populate specific fields.

| Parameter      | Description                                | Example              |
| -------------- | ------------------------------------------ | -------------------- |
| `first_name`   | The user's first name.                     | `John`               |
| `last_name`    | The user's last name.                      | `Smith`              |
| `email`        | The user's email address.                  | `jsmith@example.com` |
| `phone`        | Phone number (must be URL-encoded).        | `%2B13125551234`     |
| `template_id`  | ID of the verification template to assign. | `tmpl_MQ`            |
| `email_notify` | Set to `1` to enable email notifications.  | `1`                  |
| `sms_notify`   | Set to `1` to enable SMS notifications.    | `1`                  |

***

#### ⚡ Pro Tip: Generate Links with Excel (No-Code)

If you have a list of users in a spreadsheet (Excel or Google Sheets), you can generate these links automatically without any coding. This is perfect for onboarding batches of users quickly.

**Step 1: Organize your data** Ensure your spreadsheet has the user data in the following columns:

* **Column A:** First Name
* **Column B:** Last Name
* **Column C:** Email
* **Column D:** Phone Number (digits only, e.g., `15551234567`)

**Step 2: Use the Formula** Paste the following formula into **Column E** (or any empty column):

```excel
="https://{your_subdomain}.trustswiftly.com/admin/user/quick_create?first_name="&A2&"&last_name="&B2&"&email="&C2&"&phone=%2B"&D2&"&email_notify=1&sms_notify=1"
```

_(**Note:** Replace `{your_subdomain}` with your actual Trust Swiftly subdomain)._

**Step 3: Drag and Click** Drag the formula down for all your rows. You now have a clickable link for every user that will instantly set up their account creation page.

***

#### Example Usage

**Scenario:** You need to create a user named **John Smith**, assign the template `tmpl_MQ`, and turn on all notifications.

**Constructed URL:**

```
https://demo1.trustswiftly.com/admin/user/quick_create?first_name=John&last_name=Smith&email=jsmith@example.com&phone=%2B13125551234&template_id=tmpl_MQ&email_notify=1&sms_notify=1
```

**Result:** The administrator accesses the URL, reviews the pre-filled data, and clicks **"Create"** to finalize the account.

<figure><img src="https://1722465976-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MQXj2cAjHd66kg8IboI%2Fuploads%2FJInsdASedWtzbLSc8IeR%2Fimage.png?alt=media&#x26;token=165eb3d6-40e8-4169-8c37-4f3b38a4afe4" alt="User Creation Screen populated with data"><figcaption></figcaption></figure>
