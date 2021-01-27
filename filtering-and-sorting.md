---
description: Filtering and sorting results can help speed up responses and data collection.
---

# Filtering and Sorting

### Filtering

Each section inside the docs that supports filtering will have a list of supported filters defined and you can specify as a query parameter while making the request.

Filters should be provided as a part of the endpoint URL in the following format:

```text
?filter[FILTER_NAME]=VALUE
```

 For example, lets say that you want to get all the users that are named `John`. It can be done by providing the `search` filter while making the request:

```text
?filter[search]=John
```

There are two different types of filters, the `exact` and `partial` filters.

#### Exact Filters <a id="exact-filters"></a>

Exact filters will only return those records where a specific attribute is exactly the same as the provided filter value.

For example, if an endpoint supports an _exact_ filter for filtering out the records by status and if you provide `?filter[status]=1` query parameter, only records that have the `status` attribute set to `1` will be returned.

#### Partial Filters <a id="partial-filters"></a>

The _partial_ filters are usually used for text based fields an it will return all the records that have the provided filter vaule _anywhere_ within the attribute value.

For example, if there is a filter `name` defined for the specific resource and you provide the `?filter[name]=one` filter within the URL, the API will return all the customers from the db that contain the word `one` anywhere within their `name` attribute and not only those who has the name exactly set as `one`.

### Sorting

All sortable resources will provide the list of sortable fields that can be used for sorting the data that is being returned from the API.

To sort a resource by the specific field, just append the `?sort=FIELD` query parameter while you make the request to the API endpoint and it will sort the items in `ascending` order. To sort the items in `descending` order, prefix the field with `-` sign: `?sort=-FIELD`.

For example, if you want to sort the users in `ascending` order by the `created_at` timestamp, you should make a request to the following endpoint:

```text
/users?sort=created_at
```

If you want to sort them by the `created_at` timestamp in `descending` order, the enpoint should be updated to look like the following:

```text
/users?sort=-created_at
```

