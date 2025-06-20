---
description: Learn about API rate limits and how to work with them.
---

# Rate Limits

To ensure the stability and fair use of our platform for all users, the Trust Swiftly API imposes rate limits on incoming requests. If you send too many requests in a short period, the API will respond with an error code.

This guide explains our limits, how to monitor your usage, and how to handle rate-limiting errors gracefully.

***

#### Default Limits

Our default rate limits are designed to be sufficient for most applications.

* **300 requests per minute**
* **5 requests per second**

If your application has high-volume needs, please see the section on "Increasing Your Limits" below.

***

#### Monitoring Your Usage with HTTP Headers

Every API response includes HTTP headers that provide real-time visibility into your current rate limit status. By programmatically inspecting these headers, your application can avoid exceeding the limit.

<table><thead><tr><th width="239.99993896484375">Header</th><th>Description</th></tr></thead><tbody><tr><td><code>X-RateLimit-Limit</code></td><td>The total number of requests allowed in the current time window.</td></tr><tr><td><code>X-RateLimit-Remaining</code></td><td>The number of requests you have left in the current time window.</td></tr><tr><td><code>X-RateLimit-Reset</code></td><td>The Coordinated Universal Time (UTC) timestamp when the current time window resets.</td></tr></tbody></table>

**Example Response Headers:**

```http
HTTP/1.1 200 OK
Content-Type: application/json
X-RateLimit-Limit: 300
X-RateLimit-Remaining: 299
X-RateLimit-Reset: 1672531260
```

***

#### Handling Exceeded Limits

If you exceed the rate limit, the API will stop processing your requests and respond with an HTTP `429 Too Many Requests` error code.

```json
{
  "error_type": "api_rate_limit_error",
  "error_message": "Too Many Requests"
}
```

**Recommended Strategy: Exponential Backoff**

The best way to handle `429` errors is to implement a retry mechanism with **exponential backoff and jitter**. This pattern improves the reliability of your application by automatically retrying the failed request after waiting for a progressively longer amount of time.

**How it works:**

1. When you receive a `429` error, don't retry immediately.
2. Wait for a short, increasing duration (e.g., 1s, then 2s, then 4s, etc.).
3. Add a small, random delay ("jitter") to the wait time to prevent all instances of your application from retrying at the exact same moment.
4. After waiting, try the request again.
5. Stop retrying after a certain number of attempts to avoid an infinite loop.

**Pseudo-code Example:**

```
// A simple exponential backoff implementation
retries = 0
max_retries = 5

loop:
  try:
    response = make_api_request()
    break // Success, exit the loop

  catch (error):
    if error.status_code == 429 and retries < max_retries:
      retries += 1
      // Calculate wait time: 1s, 2s, 4s, etc. + random jitter
      wait_time = (2 ** retries) * 1000 + random_integer(0, 1000)
      wait(wait_time) // Wait in milliseconds
      continue loop // Retry the request
    else:
      // If it's not a 429 error or we've run out of retries,
      // re-throw the error to be handled by other logic.
      throw error
```

***

#### Increasing Your Limits

For applications with high-volume requirements or for specific batch processing tasks, we offer increased rate limits. This is a standard feature for our Enterprise plans.

If you anticipate needing a higher limit, please contact our support team to discuss your use case.
