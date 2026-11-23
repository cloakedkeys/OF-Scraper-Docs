---
description: Choose which creator accounts to include or exclude using usernames, user lists or blacklists.
---

# User Selection Options

## Specifying Usernames

### -u, --username (also `--usernames`, `--users`, `--user`) \[argument]

* **Selects:** Specific usernames to process, separated by commas (e.g. `name1,name2`).
* **Not case-sensitive:** Usernames match in any case. An all-digit value also matches an account ID.
* **ALL (case-sensitive):** Use `ALL` to include every available username.

**Example:** `-u user1,user2` processes only `user1` and `user2`.

### -eu, --excluded-username \[argument]

* **Excludes:** Specific usernames from processing, separated by commas (e.g. `name1,name2`).
* **Precedence:** Excluded usernames override usernames given with `-u`.

**Example:** `-u user1,user2 -eu user2` processes only `user1`.

#### With --scrape-paid

> ℹ️ **Since 3.15.0.** 3.14.7 and earlier ignore `--excluded-username` during `--scrape-paid`. See [Fork Changes](../../../fork-changes.md).

The exclusion also applies to `--scrape-paid`, for both downloads and metadata runs, so you can skip one model that keeps failing without giving up the rest of the paid scan. Names are matched case-insensitively.

```bash
ofscraper --scrape-paid --excluded-username modelname
ofscraper metadata --scrape-paid update --excluded-username modelname,othermodel
```

* A skipped model is logged (`Skipping <name>_<id>: excluded by --excluded-username`) and left out of the run's totals.
* Its profile is still looked up to learn its username.
* A deleted account can only be excluded by the username recorded for it in an earlier run. Without one it shows as `modeldeleted_<id>` and can't be matched by name.

***

## Using User Lists

### -ul, --user-list (also `--user_list`, `--userlist`, `--userlists`, `--user-lists`) \[argument]

* **Filters:** Selects users from a user list. Always takes a list name.
* **Default:** When `-ul` isn't used, the list in `default_user_list` in `config.json` (`main` unless you change it).
* **Built-in lists:** `main` (also `ofscraper.main`) means all your subscriptions. `ofscraper.active` and `ofscraper.expired` are your active and expired subscriptions. These names are reserved, so don't give any of your own lists these names.

**Example:** `-ul myUserList` processes only users in `myUserList`.

### -bl, --black-list (also `--black_list`, `--black-lists`, `--blacklist`, `--blacklists`) \[argument] (optional)

* **Excludes:** Removes all users from the given user list.
* **Default list:** None.
* **Argument behaviour:**
  * If an argument is given (e.g. `inactiveUsers`), users in that list are excluded.

**Example:** `-bl inactiveUsers` excludes users in `inactiveUsers`.
