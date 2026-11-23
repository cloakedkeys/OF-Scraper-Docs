# Price Filtering/Sort

> ⚠️ **Fallbacks are used so lists can be sorted easily.** You can eliminate fallbacks with proper filtering.

***

## Current Price

> ℹ️ Best used with `--active-subscription`.

1. If there is an active subscription and its subscription price is available, use that price.
2. If there is no active subscription or the subscription price isn't available, check for active promotions with a "claimable" tag and use the lowest subscription price among them.
3. If no "claimable" promotions are available, use the regular subscription price.
4. If none of the above provide a valid price, fall back to `0`.

***

## _Renewal Price_

> ℹ️ Best used with `--active-subscription`.

1. Use the lowest claimable promotional subscription price.
2. If no "claimable" promotions are available, use the regular subscription price.
3. If none of the above provide a valid price, fall back to `0`.

***

## Regular Price

1. Use the regular subscription price.
2. If that isn't available, it stays empty (no fallback to `0`).

***

## Promo Price

> ℹ️ Best used with `--promo-only` or `--all-promo-only`.

1. Use the lowest promotional subscription price.
2. If no promotions are available, use the regular subscription price.
3. If none of the above provide a valid price, fall back to `0`.
