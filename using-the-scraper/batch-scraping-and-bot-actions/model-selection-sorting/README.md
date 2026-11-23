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

Takes precedence over `--username`, including `--username ALL`:

```sh
ofscraper --excluded-username username
```

### Filter by regular price

```sh
ofscraper --regular-price paid
```

See [Price Filtering/Sort](price-filtering-sort.md).

***

### Advanced filtering

[User List Filter Options](../../../command-reference/shared-options/scrape-metadata-options/account-filter-args/)

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

***

## Blocking list of Names

Exclude a saved list of accounts (`--blacklist` is an alias of `--black-list` / `-bl`):

```sh
ofscraper --blacklist "tiktok"
```

> ℹ️ `--blacklist` takes precedence over `--userlist` and `--username ALL`.
