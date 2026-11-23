---
description: Filter which creator accounts are listed and processed. Filters can be combined.
---

# User List Filter Options

## Pricing Filters

> ℹ️ For details on how price filtering and sorting work, see [Price Filtering/Sort](../../../../using-the-scraper/batch-scraping-and-bot-actions/model-selection-sorting/price-filtering-sort.md).

Filter accounts by their current price, renewal price, promotional price (if available) or regular price (if available).

### -cp, --current-price \[argument]

* **Possible choices:**
  * `paid`: Accounts with a paid current price.
  * `free`: Accounts with a free current price.

### -rp, --renewal-price \[argument]

* **Possible choices:**
  * `paid`: Accounts with a paid renewal price.
  * `free`: Accounts with a free renewal price.

### -pp, --promo-price \[argument]

Uses the lowest promotional price, claimable or not, otherwise the regular price.

* **Possible choices:**
  * `paid`: Accounts with a paid price.
  * `free`: Accounts with a free price.

### -gp, --regular-price \[argument]

* **Possible choices:**
  * `paid`: Accounts with a regular price (if applicable).
  * `free`: Accounts without a regular price (if applicable).

***

## Account Flags

Filter accounts by specific flags or properties.

### -lo, --last-seen-only

* **Filters:** Accounts where the "last seen" date/time is visible.

### -ls, --last-seen-skip

* **Filters:** Accounts where the "last seen" date/time is hidden.

### -po, --promo-only

* **Filters:** Accounts with any claimable promotional price.

### -ps, --promo-skip

* **Filters:** Accounts without any claimable promotional price.

### -ao, --all-promo-only

* **Filters:** Accounts with any promotional price, claimable or not.

### --all-promo-skip

* **Filters:** Accounts without any promotional price, claimable or not.

***

## Subscription Type

Filter accounts by their subscription status.

### -fo, --free-trial-only

* **Filters:** Accounts currently in a free trial (normally paid accounts).

### -fs, --free-trial-skip

* **Filters:** Accounts not currently in a free trial (normally paid accounts).

### -ts, --active-subscriptions

* **Filters:** Accounts with active, non-expired subscriptions.

### -es, --expired-subscription

* **Filters:** Accounts with expired subscriptions.

### -ro, --renew-on

* **Filters:** Accounts with the "renew" flag enabled.

### -rf, --renew-off

* **Filters:** Accounts with the "renew" flag disabled.
