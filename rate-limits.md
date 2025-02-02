---
description: Learn about API rate limits and how to work with them.
---

# Rate Limits

We use rate limiting to safeguard the stability of our API. Our rate limiter allows up to 300 requests per minute and 10 requests per second. You can see your current rate limit by looking at the HTTP header `x-ratelimit-remaining`. To increase this limit, please [contact us](https://trustswiftly.com/contact-us/).

Any request over the limit will return a 429 Too Many Requests error.
