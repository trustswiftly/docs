# Configure self verifications

Self verifications are a quick way to getting started with Trust Swiftly. It requires no code or integration but would require additional steps for your users to create an account to complete the verifications. Using another integration option can be added at a later point to further automate the process.

To enable self sign up for getting verified you can enable the setting at [https://{sub-domain}.trustswiftly.com/settings/auth](https://{sub-domain}.trustswiftly.com/settings/auth)&#x20;

1. Enable Allow customer sign up and click Update Settings to save.
2. Select a default verification template for users to complete. i.e. once registered the user must complete an ID + Email verification.
3. Notify you users about this self sign up process at this link [https://{sub-domain}.trustswiftly.com/signup](https://{sub-domain}.trustswiftly.com/signup). For example, add a link or button on your site that directs your users to Trust Swiftly to verify themselves.

```markup
<a href="https://{sub-domain}.trustswiftly.com/signup" target="_blank">
Verify yourself at Trust Swiftly</a>
```

![Options to enable for self sign up](<../.gitbook/assets/image (13).png>)
