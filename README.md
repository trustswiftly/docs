---
description: >-
  This documentation will show you how to integrate Trust Swiftly into your Web
  Application and communicate with our private API.
---

# Developer Documentation

### Quickstart

| Integration Options (Web)                                                                                                         | Details                                                                                                                                                                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><a href="getting-an-api-key.md">Rest API</a></p><p> (Average 3-7 day effort to setup)</p>                                      | Use the API to programmatically add users and modify required verifications. The API can be used by using the magic link to create a simple verification button. You are not able to directly send us images to analyze for documents. All verifications must be completed through the hosted link for security. |
| [No Code Managed](hosted/share-hosted-link.md)                                                                                    | Use the no code integration to share a simple link through email, chat, or SMS which will redirect the user to a hosted page to complete verifications. This method requires an admin to add the user to verify manually and then review them once complete.                                                     |
| [iOS and Android Apps](web/webview-ios-and-android.md)                                                                            | Use iOS and Android webview implementations to integrate your native app with Trust Swiftly.                                                                                                                                                                                                                     |
| <p><a href="self-sign-up-and-create-autofill/configure-self-verifications.md">No Code Self-Signup</a> </p><p>(3-minute setup)</p> | Direct users to our signup page to register details themselves for onboarding and then allow them to complete the template verification request. This method requires no upfront work and can be used as customer identity management platform.                                                                  |

Each method to integrate above has pros and cons depending on your use case. For the simplest and fastest to manage process the no code self-signup works well. For more custom options we recommend our API.
