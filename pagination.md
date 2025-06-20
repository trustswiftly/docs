---
description: >-
  All top-level API endpoints have support for bulk fetches via "list" API
  methods.
---

# Pagination

#### Handling Paginated Responses

Endpoints that can return a large number of items (like listing users or documents) are **paginated**. This means that instead of returning all results in a single, massive response, the data is returned in "pages."

You must be prepared to handle this paginated structure to retrieve all the results you need. All paginated endpoints in the Trust Swiftly API share the same consistent structure.

***

#### Understanding the Paginated Response

A paginated response contains three top-level objects: `data`, `links`, and `meta`.

| Key     | Description                                                                   |
| ------- | ----------------------------------------------------------------------------- |
| `data`  | An array containing the list of resource objects for the current page.        |
| `links` | An object containing ready-to-use URLs for navigating through the pages.      |
| `meta`  | An object containing metadata about the paginated list, such as total counts. |

**The `links` Object**

This object provides full URLs for easy navigation.

<table><thead><tr><th width="265.33331298828125">Link</th><th>Description</th></tr></thead><tbody><tr><td><code>first</code></td><td>The URL for the first page of results.</td></tr><tr><td><code>last</code></td><td>The URL for the last page of results.</td></tr><tr><td><code>prev</code></td><td>The URL for the previous page. Will be <code>null</code> if you are on the first page.</td></tr><tr><td><code>next</code></td><td>The URL for the next page. Will be <code>null</code> if you are on the last page.</td></tr></tbody></table>

> **Best Practice:** For the most robust integration, your application should use the full URLs provided in the `links` object for navigation rather than constructing your own. This protects your application from potential future changes to the URL structure.

**The `meta` Object**

This object provides detailed information about the current state of the pagination.

<table><thead><tr><th width="228">Field</th><th>Description</th></tr></thead><tbody><tr><td><code>current_page</code></td><td>The page number you are currently viewing.</td></tr><tr><td><code>from</code></td><td>The item number of the first result on the current page.</td></tr><tr><td><code>last_page</code></td><td>The total number of pages available.</td></tr><tr><td><code>path</code></td><td>The base URL for the resource.</td></tr><tr><td><code>per_page</code></td><td>The number of items requested per page.</td></tr><tr><td><code>to</code></td><td>The item number of the last result on the current page.</td></tr><tr><td><code>total</code></td><td>The total number of items in the entire collection.</td></tr></tbody></table>

***

#### Controlling Pagination

You can control pagination using query parameters in your request URL.

**Changing the Page Size (`per_page`)**

To specify how many records you want per page, append the `per_page` parameter.

* **Default:** 15 items per page.
* **Maximum:** 100 items per page. If you request more than 100, the API will return 100.

**Example: Requesting 50 users per page.**`GET /api/users?per_page=50`

**Requesting a Specific Page (`page`)**

To navigate to a specific page, use the `page` parameter.

**Example: Requesting the second page of 50 users.**`GET /api/users?per_page=50&page=2`

***

#### Complete Example

**Request**

Here is a `curl` example requesting the first page of users, with a page size of 2.

```bash
curl --request GET \
  --url 'https://{sub-domain}.trustswiftly.com/api/users?per_page=2&page=1' \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Accept: application/json'
```

**Response**

```json
{
    "data": [
        {
            "id": 1,
            "first_name": "John",
            "last_name": "Doe",
            // ... more user fields
        },
        {
            "id": 2,
            "first_name": "Jane",
            "last_name": "Smith",
            // ... more user fields
        }
    ],
    "links": {
        "first": "https://{sub-domain}.trustswiftly.com/api/users?page=1",
        "last": "https://{sub-domain}.trustswiftly.com/api/users?page=5",
        "prev": null,
        "next": "https://{sub-domain}.trustswiftly.com/api/users?page=2"
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 5,
        "path": "https://{sub-domain}.trustswiftly.com/api/users",
        "per_page": 2,
        "to": 2,
        "total": 10
    }
}
```
