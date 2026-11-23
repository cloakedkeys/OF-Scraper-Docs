# Model Filtering/Sorting

***

## Filter/Sort List By Price

[Price Filtering/Sort](price-filtering-sort.md)

***

## Selecting Specific models from command-line

Pass a comma-separated list of creators to scrape:

```sh
ofscraper --username name1,name2
```

`--username` (`-u`; also `--usernames`, `--users`, `--user`) isn't case-sensitive: usernames match in any case, and an all-digit value also matches an account ID.

#### Selecting all users

```sh
ofscraper --username ALL
```

`ALL` is affected by filters and is case-sensitive.

***

## Filtering username list

These settings can also be changed interactively when using prompts. See [Using Prompts](../../using-prompts/).

Filters don't change which usernames are fetched; they only affect which usernames are displayed.

> ℹ️ To fetch a specific group of usernames, create a list on OnlyFans and pass `--userlist` or `--blacklist`.

### Version >2.1

`--username` takes precedence over filters, so only the specified creators are used. The exception is `ALL`, which is still filtered.

### Restrict by account type

Limit the scraper to free accounts only:

```sh
ofscraper --current-price free --username ALL
```

### Restrict by subscription status

Scrape messages from expired subscriptions:

```sh
ofscraper --expired-subscription --posts messages --username ALL --action download
```

### Restrict by renewal status

`--renew-off` (`-rf`) keeps every account that isn't set to renew, including expired ones (`--renew-on` / `-ro` keeps accounts set to renew). Add `--active-subscription` to limit it to active accounts:

```sh
ofscraper --renew-off --active-subscription --username ALL
```

***

### Combining filters

Scrape paid active accounts set to expire:

```sh
ofscraper --current-price paid --active-subscription --renew-off --username ALL
```

Or scrape free active accounts only:

```sh
ofscraper --current-price free --active-subscription --username ALL
```

### Exclude specific models

`--excluded-username` (`-eu`) takes a comma-separated list and takes precedence over `--username`, including `--username ALL`:

```sh
ofscraper --excluded-username username
```

For example, `-u user1,user2 -eu user2` processes only `user1`.

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

### Filter by regular price

```sh
ofscraper --regular-price paid
```

See [Price Filtering/Sort](price-filtering-sort.md).

***

### Advanced filtering

Every filter, with its short form, is in [User List Filter Options](../../../reference/cli.md#user-list-filter-options) and [Advanced User List Filter Options](../../../reference/cli.md#advanced-user-list-filter-options). Filters can be combined.

**Price:** `--current-price`, `--renewal-price`, `--promo-price` and `--regular-price` take `paid` or `free`. `--promo-price` uses the lowest promotional price, claimable or not, otherwise the regular price. The `-min` and `-max` forms (for example `--promo-price-max`) keep accounts whose price is at or above, or at or below, the given value. See [Price Filtering/Sort](price-filtering-sort.md) for how each price is worked out.

**Account flags** (pick one of each pair):

| Keep accounts | Option |
|---|---|
| Whose "last seen" time is visible / hidden | `--last-seen-only` / `--last-seen-skip` |
| With / without a claimable promotional price | `--promo-only` / `--promo-skip` |
| With / without any promotional price, claimable or not | `--all-promo-only` / `--all-promo-skip` |
| In / not in a free trial (normally paid accounts) | `--free-trial-only` / `--free-trial-skip` |
| With an active / expired subscription | `--active-subscription` / `--expired-subscription` |
| With the "renew" flag on / off | `--renew-on` / `--renew-off` |

**Dates:** `--last-seen-after`, `--last-seen-before`, `--expired-after`, `--expired-before`, `--subscribed-after` and `--subscribed-before` take a date. See [Valid Inputs](../basic-actions/selecting-posts/README.md#valid-inputs) for the formats.

* The "last seen" time isn't available for every account.
* When a model is set to renew, the expired date (and the `expired` sort) refers to the renewal date.
* The subscription date isn't always reliable for expired accounts. Consider `--expired-after` (`-ea`) or `--expired-before` (`-eb`) instead.

***

## Sorting username list

`--sort` (`-st`) accepts `name`, `subscribed`, `expired`, `current-price`, `renewal-price`, `regular-price`, `promo-price`, and `last-seen`. The default is `name`, ascending.

> ℹ️ Sorting affects the order of scraping, not just the order shown in the prompt menu.

### sort by account expiring date

```sh
ofscraper --sort expired
```

### sort by account subscribed date

```sh
ofscraper --sort subscribed
```

#### sort by account name

```sh
ofscraper --sort name
```

### sort by promotional prices

```sh
ofscraper --sort promo-price
```

See [Price Filtering/Sort](price-filtering-sort.md).

### desc option

Sorting is ascending by default. Add `--desc` to sort in descending order:

```sh
ofscraper --sort current-price --desc
```

***

## Retrieving specific list

Switch from your main OnlyFans list to a saved list of accounts (`--userlist` is an alias of `--user-list` / `-ul`):

```sh
ofscraper --userlist "tiktok"
```

Combine multiple lists by repeating `--userlist`:

```sh
ofscraper --userlist "tiktok" --userlist "tiktok2"
```

* Without `--userlist`, the list in `default_user_list` in `config.json` is used (`main` unless you change it).
* Built-in lists: `main` (also `ofscraper.main`) means all your subscriptions. `ofscraper.active` and `ofscraper.expired` are your active and expired subscriptions. These names are reserved, so don't give any of your own lists these names.

***

## Blocking list of Names

Exclude a saved list of accounts (`--blacklist` is an alias of `--black-list` / `-bl`):

```sh
ofscraper --blacklist "tiktok"
```

> ℹ️ `--blacklist` takes precedence over `--userlist` and `--username ALL`.
