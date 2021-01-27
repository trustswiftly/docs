# Errors

 Trust Swiftly uses conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed given the information provided \(e.g., a required parameter was omitted, a user doesn't exist, etc.\). Codes in the `5xx` range indicate an error with Trust Swiftly's servers \(these are rare\).

### Get Users Failure

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Create User Failure

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

### Get Users Failure

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Get Users Failure

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Get Users Failure

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Get Users Failure

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```

### Get Users Failure

```http
{
  "error_code": "004",
  "error_message": "User Not Found"
}
```



