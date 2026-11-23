---
description: Fine-tune caching, decryption, dynamic rules and auth failure behaviour.
---

# Advanced Program Options

## Caching and API Calls

### -nc, --no-cache

* **Disables:** Reading from and writing to the program's cache (such as stored keys and file sizes).
* **Effect:** Forces fresh sequential API calls even when data is cached. Ensures you get the latest information, though runs may be slower.
* **Default:** `False` (cache is enabled).

### -nca, --no-api-cache

* **Effect:** Forces sequential API calls even when data is cached within the current session. Unlike `--no-cache`, this affects only API requests rather than all uses of the cache.
* **Default:** `False` (API cache is enabled for the current session).

***

## Configuration Overrides

### -k, --key-mode \[argument]

* **Overrides:** The key mode setting in `config.json`.
* **Possible values:**
  * `manual`
  * `cdrm` (deprecated: its service no longer works; use `manual`)
* **Example:** `-k manual`.
* **Not available in:** `metadata` and `db`.

### -pk, --private-key \[argument]

* **Overrides:** The `private-key` setting in `config.json`.
* **Sets:** The path to the private key file used by `manual` key mode.

### -ci, --client-id \[argument]

* **Overrides:** The `client-id` setting in `config.json`.
* **Sets:** The path to the client ID file used by `manual` key mode.

### -dr, --dynamic-rules \[argument]

* **Overrides:** The `dynamic-rules` setting in `config.json`.
* **Used for:** Signing API requests.
* **Default:** None (`dynamic-mode-default` from `config.json` is used).
* **Also:** `--dynamic-rule`.
* **Possible values:**
  * `digitalcriminals` (aliases: `datawhores`, `dc`, `digital`, `digitals`, `digitalcriminal`)
  * `manual`
  * `generic`
  * `xagler`
  * `rafa`
* **Example:** `-dr digitalcriminals`.
* **Note:** Available values may change as sources are updated or removed.

***

## Additional Options

### -up, --update-profile

* **Retrieves:** Up-to-date profile information directly from the API, bypassing the cache.
* **Cache update:** Profile information is typically cached for about a day. Use this option when you need the latest data.

### -al, --auth-fail (also `--auth-quit`)

* **Effect:** Quits on authentication failure rather than prompting.
* **Default:** `False`.

