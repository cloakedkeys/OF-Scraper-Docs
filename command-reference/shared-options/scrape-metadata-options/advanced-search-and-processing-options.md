---
description: Control how usernames are looked up and the order in which users are processed.
---

# Advanced Search & Processing Options

## Username Search Behaviour

These options control how usernames are looked up and processed during actions.

### -uf, --users-first (also `--user-first`, `--usersfirst`, `--userfirst`)

* **Prioritises:** Scrapes all users first instead of processing them one at a time.
* **Effect:** Gathers all required data before downloading or processing metadata.
* **Default:** `False` (users are processed one by one).

### -fi, --username-individual-search (also `--user-individual-search`)

* **Enforces:** Looks up each username given with `--username` in a separate request.
* **Default:** Depends on the number of `--username` values and the number of subscriptions on the account.
* **Use case:** Can be faster than retrieving usernames in bulk.

### -fl, --username-list-search (also `--user-list-search`)

* **Processes:** Searches the entire user list from the enabled `userlist` config or `--user-list` argument.
* **Effect:** Filters usernames from the fetched list.
* **Default:** Depends on the number of `--username` values and the number of subscriptions on the account.
* **Use case:** Useful when retrieving a large number of users.

**Note:** Using `-fi` can make many individual requests and hit rate limits.
