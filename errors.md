# Errors

 Trust Swiftly uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed given the information provided \(e.g., a required parameter was omitted, a user doesn't exist, etc.\). Codes in the `5xx` range indicate an error with Trust Swiftly's servers \(these are rare\).

| Error Code | Description |
| :--- | :--- |
| 000 | API Key Wrong or Unauthorized User |
| 101 | Validation Failed |
| 002 | Invalid templateId provided |
| 003 | Invalid or No Data Provided for Update |
| 004 | User Not Found |
| 1001 | Resource Not Found |
| 999 | Internal Error |

### Get Users

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Create User

{% tabs %}
{% tab title="101" %}
```http
{
  "error_code": "101",
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
    "error_code": "002",
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
    "error_code": "004",
    "error_message": "User Not Found"
}
```
{% endtab %}

{% tab title="003" %}
```
{
    "error_code": "003",
    "error_message": "Invalid or No Data Provided for Update"
}
```
{% endtab %}
{% endtabs %}

### Delete User

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Magic Link

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Generate Token

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Delete Token

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```



