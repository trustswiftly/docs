---
description: This page describes various error responses with our API.
---

# Errors

#### Error Handling

Trust Swiftly uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the `2xx` range indicate success. Codes in the `4xx` range indicate a client-side error. Codes in the `5xx` range indicate an error with Trust Swiftly's servers.

When an error occurs, the API will return a JSON object containing a specific `error_type` and a message to help you diagnose the issue.

***

#### HTTP Status Codes Summary

<table><thead><tr><th>Status Code</th><th width="158.333251953125">Meaning</th><th>Description</th></tr></thead><tbody><tr><td><code>200 OK</code></td><td>OK</td><td>Everything worked as expected.</td></tr><tr><td><code>201 Created</code></td><td>Created</td><td>The resource was created successfully.</td></tr><tr><td><code>400 Bad Request</code></td><td>Bad Request</td><td>The request was unacceptable, often due to malformed syntax or missing data.</td></tr><tr><td><code>401 Unauthorized</code></td><td>Unauthorized</td><td>No valid API key was provided or the key is invalid.</td></tr><tr><td><code>404 Not Found</code></td><td>Not Found</td><td>The requested resource (like a user) does not exist.</td></tr><tr><td><code>422 Unprocessable Entity</code></td><td>Unprocessable Entity</td><td>The request was well-formed, but the server was unable to process it due to validation errors.</td></tr><tr><td><code>500</code> / <code>5xx</code></td><td>Server Error</td><td>Something went wrong on Trust Swiftly's end.</td></tr></tbody></table>

***

#### Error Types & Examples

Here is a guide to the specific `error_type` codes returned by the API.

**`api_auth_error`**

* **HTTP Status:** `401 Unauthorized`
* **When:** This occurs if your API key is missing, incorrect, or disabled.
*   **Response:**

    ```json
    {
      "error_type": "api_auth_error",
      "error_message": "Unauthenticated."
    }
    ```

***

**`api_user_error` or `api_resource_error`**

* **HTTP Status:** `404 Not Found`
* **When:** The resource you are trying to access does not exist. This commonly occurs when using an incorrect `user_id` or other resource identifier.
*   **Response:**

    ```json
    {
      "error_type": "api_user_error",
      "error_message": "User Not Found"
    }
    ```

***

**`api_validation_error`**

* **HTTP Status:** `422 Unprocessable Entity`
* **When:** This is the most common error when creating or updating resources. It means the data provided failed server-side validation. The `errors` object gives a field-by-field breakdown of what went wrong.
*   **Response:**

    ```json
    {
      "error_type": "api_validation_error",
      "error_message": "The given data was invalid.",
      "errors": {
        "email": [
          "The email has already been taken."
        ],
        "reference_id": [
          "The reference id field is required."
        ]
      }
    }
    ```

***

**`api_template_error`**

* **HTTP Status:** `422 Unprocessable Entity`
* **When:** The `template_id` you provided is invalid, does not exist, or is not accessible to your account.
*   **Response:**

    ```json
    {
      "error_type": "api_template_error",
      "error_message": "Invalid templateId provided."
    }
    ```

***

**`api_invalid_error`**

* **HTTP Status:** `400 Bad Request`
* **When:** The request is malformed or missing data in a way that prevents processing. This is a more general error than a validation failure.
*   **Response:**

    ```json
    {
      "error_type": "api_invalid_error",
      "error_message": "Invalid or No Data Provided for Update"
    }
    ```

***

**`api_internal_error`**

* **HTTP Status:** `500 Internal Server Error`
* **When:** An unexpected error occurred on Trust Swiftly's servers. These are rare. If you consistently receive a 500 error, please contact support.
*   **Response:**

    ```json
    {
      "error_type": "api_internal_error",
      "error_message": "Internal Server Error"
    }
    ```
