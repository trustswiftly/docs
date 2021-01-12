---
description: >-
  This sample call, which shows the Users API, includes a bearer token in the
  Authorization request header.
---

# Authentication

#### Example Authenticated Request

```text
curl --location --request GET 'https://{sub-domain}.trustswiftly.com/account/api/users' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {api_key}'
```

