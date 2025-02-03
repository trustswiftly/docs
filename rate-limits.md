---
description: Learn about API rate limits and how to work with them.
---

# Rate Limits

We use rate limiting to safeguard the stability of our API. Our default rate limiter allows up to 300 requests per minute and 5 requests per second.&#x20;

You can see your current rate limit by looking at the HTTP header `x-ratelimit-remaining`. To increase this limit, please [contact us](https://trustswiftly.com/contact-us/). (Enterprise plans allow for much higher rate limits.)

Any request over the limit will return a 429 Too Many Requests error.
