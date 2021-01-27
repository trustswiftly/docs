---
description: >-
  All top-level API endpoints have support for bulk fetches via "list" API
  methods.
---

# Pagination

Some endpoints will return data in a paginated list. A paginated response will look similar to this:

```text
{
    "data": [
        //...
    ],
    "links": {
        "first": "https://yourwebsite.com/account/api/users?page=1",
        "last": "https://yourwebsite.com/account/api/users?page=1",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "http://yourwebsite.com/account/api/users",
        "per_page": 15,
        "to": 15,
        "total": 15
    }
}
```

As per the example above, each paginated response will have the `data` array, which contains all the items from the specific page, a `links` object with full URLs for fetching `first`, `last`, `prev` and `next` pages, and the `meta` object which contains all the info about the resource you are paginating.

Some endpoints allow you to specific number of records that you want to receive per page. To achieve that you can append the `per_page=X` parameter to the URL of the request. For example, if you want to request `50` users per page, the URL parameters should look like the following:

```text
/users?per_page=50
```

Pagination limit is set to `100` for most resources which means that you cannot request more than `100` records per page. If you provide a larger number, it will be ignored and `100` records per page will be returned.

To request a different page, just append the `page=X` parameter to the URL. For our customers example above, you can get the second page like following:

```text
/users?per_page=50&page=2
```

