---
description: Filter creator accounts by price ranges and activity or subscription dates.
---

# Advanced User Filters

## Advanced Pricing Filters

Target accounts by price ranges across promotional, regular, current and renewal pricing.

### -ppm, --promo-price-max \[argument]

* **Filters:** Accounts where the lowest available promotional price is at or below the given value.

### -ppn, --promo-price-min \[argument]

* **Filters:** Accounts where the lowest available promotional price is at or above the given value.

### -gpm, --regular-price-max \[argument]

* **Filters:** Accounts where the regular price (if available) is at or below the given value.

### -gpn, --regular-price-min \[argument]

* **Filters:** Accounts where the regular price (if available) is at or above the given value.

### -cpm, --current-price-max \[argument]

* **Filters:** Accounts where the current price is at or below the given value.

### -cpn, --current-price-min \[argument]

* **Filters:** Accounts where the current price is at or above the given value.

### -rpm, --renewal-price-max \[argument]

* **Filters:** Accounts where the renewal price (if applicable) is at or below the given value.

### -rpn, --renewal-price-min \[argument]

* **Filters:** Accounts where the renewal price (if applicable) is at or above the given value.

***

## Advanced Account Attributes

Target accounts by activity or subscription dates. See [Valid date inputs](../../../../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/selecting-posts/README.md#valid-inputs) for accepted date formats.

### -lsa, --last-seen-after \[argument]

* **Filters:** Accounts where the "last seen" date/time is at or after the given date.

### -lsb, --last-seen-before \[argument]

* **Filters:** Accounts where the "last seen" date/time is at or before the given date.

**Note:** The "last seen" date/time isn't always available for every account.

> ℹ️ **When a model is set to renew, the expired date refers to the renewal date.**

### -ea, --expired-after \[argument]

* **Filters:** Accounts with an expiration or renewal date at or after the given date.

### -eb, --expired-before \[argument]

* **Filters:** Accounts with an expiration or renewal date at or before the given date.

> ℹ️ **The subscription date isn't always reliable for expired accounts. Consider using `-ea` or `-eb` instead.**

### -sa, --subscribed-after \[argument]

* **Filters:** Accounts with a subscription date after the given date.

### -sb, --subscribed-before \[argument]

* **Filters:** Accounts with a subscription date at or before the given date.
