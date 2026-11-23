---
description: Control the display and processing order of creator accounts.
---

# Model Sorting & Processing Options

> ℹ️ **When a model is set to renew, the `expired` option refers to the renewal date.**

## Sorting Criteria

### -st, --sort \[argument]

* **Controls:** The display and processing order of the model list.
* **Possible choices:**
  * `name`: Model name (default).
  * `subscribed`: Whether the model is currently subscribed.
  * `expired`: Renewal or expiration date.
  * `current-price`: Current price.
  * `promo-price`: Promotional price (if available).
  * `regular-price`: Regular price (if available).
  * `renewal-price`: Renewal price (if applicable).
  * `last-seen`: When the model was last seen.
* **Example:** `-st expired` processes models with expiring subscriptions first.

### -ds, --desc

* **Arranges:** Sorts the model list in descending order.
* **Default:** `False` (ascending order).
* **Use case:** Prioritise models at the end of the list (for example, `-st last-seen -ds`).
