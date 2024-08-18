# Prefill User Creation

Use the user parameter to dynamically preset user values by making a request with data such as email, phone, first\_name, last\_name, email\_notify, sms\_notify, template\_id.

```
/user/quick_create
```

All attributes are optional. You only need to include keys for form fields you want prefilled. Admins can still edit attributes after they're prefilled.

For example a request to autofill is sent here:

[`https://demo1.trustswiftly.com/user/quick_create?first_name=John&last_name=Smith&phone=+131212345678&email=test@example.com&sms_notify=1&email_notify=1&template_id=tmpl_MQ`](https://demo1.trustswiftly.com/user/quick\_create?first\_name=John\&last\_name=Smith\&phone=+131212345678\&email=test@example.com\&sms\_notify=1\&email\_notify=1\&template\_id=tmpl\_MQ)

The user create page would have the information filled out and the admin would only need to click Create after reviewing the prefilled information.

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>
