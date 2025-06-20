---
description: Filtering and sorting results can help speed up responses and data collection.
---

# Filtering and Sorting

You can refine the results from list endpoints by using `filter` and `sort` query parameters. This allows you to request only the data you need and in the order you want it.

These parameters can be combined with each other and with our Pagination parameters for powerful, precise queries.

***

#### Filtering Results

To filter a list, use the `filter` query parameter with a specific field name in square brackets.

**Syntax:**`?filter[parameter_name]=value`

There are two types of filters available, depending on the parameter. Each endpoint's documentation will specify which filters are available and what type they are.

<table><thead><tr><th width="171.66668701171875">Filter Type</th><th>Description</th><th>Example Use Case</th></tr></thead><tbody><tr><td><strong>Exact Match</strong></td><td>Returns records where the attribute exactly matches the provided value.</td><td>Filtering for a specific status, like <code>active</code> users.</td></tr><tr><td><strong>Partial Match</strong></td><td>Performs a "wildcard" or "contains" search on a text-based field.</td><td>Searching for a user by a piece of their name or email.</td></tr></tbody></table>

**Example: Filtering by a search term**

This request will return all users where the searchable fields (like name or email) contain the string "John".

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?filter[search]=John' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

***

#### Sorting Results

To sort a list, use the `sort` query parameter followed by the field name you wish to sort by.

<table><thead><tr><th width="197.66668701171875">Sort Order</th><th width="185.6666259765625">Syntax</th><th>Description</th></tr></thead><tbody><tr><td><strong>Ascending</strong></td><td><code>?sort=field_name</code></td><td>Sorts from A-Z, or oldest to newest.</td></tr><tr><td><strong>Descending</strong></td><td><code>?sort=-field_name</code></td><td><strong>Prefix with a minus sign (-)</strong>. Sorts from Z-A, or newest to oldest.</td></tr></tbody></table>

**Example: Sorting by creation date**

This request will return all users sorted by their creation date, with the newest users appearing first.

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?sort=-created_at' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

***

#### Combining Operations

You can combine filtering, sorting, and pagination into a single request by separating the parameters with an ampersand (`&`).

**Example: Complex Query**

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

***

#### Available Fields per Endpoint

This page provides a general guide. The specific fields that you can filter or sort by are defined in the documentation for each individual API endpoint.

**Example for the `/users` endpoint:**

| Parameter Name | Filter Type | Sortable |
| -------------- | ----------- | -------- |
| `status`       | Exact       | Yes      |
| `search`       | Partial     | No       |
| `created_at`   | N/A         | Yes      |
| `email`        | Exact       | Yes      |
