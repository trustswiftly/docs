---
description: >-
  Filtering and sorting results can help speed up responses and data collection
  by allowing you to request only the data you need.
---

# Filtering and Sorting Users

You can refine the results from list endpoints by using `filter` and `sort` query parameters. This allows you to request only the data you need and in the order you want it.

These parameters can be combined with each other and with our Pagination parameters for powerful, precise queries.

***

**Filtering Results**

To filter a list, use the `filter` query parameter with a specific field name in square brackets.

**Syntax:** `?filter[parameter_name]=value`

There are two types of filters available, depending on the parameter. Each endpoint's documentation will specify which filters are available and what type they are.

| Filter Type       | Description                                                             | Example Use Case                                        |
| ----------------- | ----------------------------------------------------------------------- | ------------------------------------------------------- |
| **Exact Match**   | Returns records where the attribute exactly matches the provided value. | Filtering for a specific status, like `active` users.   |
| **Partial Match** | Performs a "wildcard" or "contains" search on a text-based field.       | Searching for a user by a piece of their name or email. |

**Example: Filtering by a partial search term**

This request will return all users where the searchable fields (like name or email) contain the string "John".

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?filter[search]=John' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

***

**Sorting Results**

To sort a list, use the `sort` query parameter followed by the field name you wish to sort by.

| Sort Order     | Syntax              | Description                                                            |
| -------------- | ------------------- | ---------------------------------------------------------------------- |
| **Ascending**  | `?sort=field_name`  | Sorts from A-Z, or oldest to newest.                                   |
| **Descending** | `?sort=-field_name` | **Prefix with a minus sign (-)**. Sorts from Z-A, or newest to oldest. |

**Example: Sorting by creation date**

This request will return all users sorted by their creation date, with the newest users appearing first.

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?sort=-created_at' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

***

**Combining Operations**

You can combine filtering, sorting, and pagination into a single request by separating the parameters with an ampersand (`&`).

**Example 1: Filtering and Sorting**

This request demonstrates a powerful combination:

1. **Filters** for users with an `active` status.
2. **Sorts** the results to show the newest active users first.
3. **Paginates** the results to show only the first 10.

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?filter[status]=active&sort=-created_at&per_page=10' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

**Example 2: Combining Multiple Filters**

This request combines two different filters to find users who have "john" in their name/username **AND** whose email is exactly `support@example.com`.

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?filter[search]=john&filter[email]=support@example.com' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

***

**Available Fields for `/api/users`**

The following tables outline the specific filtering and sorting capabilities for the `/users` endpoint.

**Filtering:**

| Parameter        | Filter Type   | Description                                                                                        |
| ---------------- | ------------- | -------------------------------------------------------------------------------------------------- |
| `filter[search]` | Partial Match | Performs a "contains" search across the `username`, `first_name`, `last_name`, and `email` fields. |
| `filter[email]`  | Exact Match   | Finds a user with the exact email address specified.                                               |
| `filter[status]` | Exact Match   | Finds all users with a specific status (e.g., `active`, `banned`, `unconfirmed`).                  |

**Sorting:**

| Parameter | Available Fields                                                               |
| --------- | ------------------------------------------------------------------------------ |
| `sort`    | `id` (default), `first_name`, `last_name`, `email`, `created_at`, `updated_at` |
