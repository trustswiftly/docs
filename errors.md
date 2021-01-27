---
description: This page describes various error responses with our API.
---

# Errors

 Trust Swiftly uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed given the information provided \(e.g., a required parameter was omitted, a user doesn't exist, etc.\). Codes in the `5xx` range indicate an error with Trust Swiftly's servers \(these are rare\).

### HTTP Status Codes <a id="http-status-codes"></a>

| HTTP Status Code | Status Message | Description |
| :--- | :--- | :--- |
| 200 | OK | Everything worked as expected. |
| 201 | Created | Resource was created successfully. |
| 400 | Bad Request | The request was unacceptable, often due to missing a required parameter. |
| 401 | Unauthorized | No valid API key provided. |
| 403 | Forbidden | Accessing the resource is forbidden for this user. |
| 404 | Not Found | The requested resource doesn't exist. |
| 422 | Unprocessable Entity | Required fields are missing or cannot be processed. |
| 500, 502, 503, 504 | Server Errors | Something went wrong on Trust Swiftly's end. |

### Error Types

| **Error** Type | **Description** |
| :--- | :--- |
| api\_auth\_error | API Key Wrong or Unauthorized User |
| api\_validation\_error | Validation Failed |
| api\_template\_error | Invalid templateId provided |
| api\_invalid\_error | Invalid or No Data Provided for Update |
| api\_user\_error | User Not Found |
| api\_resource\_error | Resource Not Found |
| api\_internal\_error | Internal Error |

### Get Users

```http
{
  "error_type": "api_user_error",
  "error_message": "User Not Found"
}
```

### Create User

{% tabs %}
{% tab title="101" %}
```http
{
  "error_type": "api_invalid_error",
  "error_message": "The given data was invalid.",
  "errors": {
    "email": [
      "The email has already been taken."
    ]
  }
}
```
{% endtab %}

{% tab title="002" %}
```
{
    "error_code": "api_template_error",
    "error_message": "Invalid templateId provided."
}
```
{% endtab %}
{% endtabs %}

### Update User

{% tabs %}
{% tab title="004" %}
```http
{
    "error_type": "api_user_error",
    "error_message": "User Not Found"
}
```
{% endtab %}

{% tab title="003" %}
```
{
    "error_code": "api_invalid_error",
    "error_message": "Invalid or No Data Provided for Update"
}
```
{% endtab %}
{% endtabs %}

### Delete User

```http
{
  "error_type": "api_user_error",
  "error_message": "User Not Found"
}
```

### Magic Link

```http
{
  "error_type": "api_user_error",
  "error_message": "User Not Found"
}
```

### Generate Token

```http
{
  "error_type": "api_user_error",
  "error_message": "User Not Found"
}
```

### Delete Token

```http
{
  "error_type": "api_user_error",
  "error_message": "User Not Found"
}
```



