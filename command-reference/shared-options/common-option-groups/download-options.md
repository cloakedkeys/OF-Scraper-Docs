---
description: Fine-tune how the program handles downloads.
---

# Download Options

## Download Configuration Overrides

> ℹ️ For help choosing thread and semaphore counts, see [Values to Pick](../../../getting-started/config-options/performance-options/values-to-pick.md).

### -db, --downloadbars (also `--download-bars`, `--download-bar`)

* **Overrides:** The `downloadbars` setting in `config.json`.
* **Default:** `None`.
* **Available in:** The main program and `metadata` only.

### -sd, --downloadsem (also `--downloadsems`, `--download-sems`, `--download-sem`, `--sems`, `--sem`) \[argument]

* **Overrides:** The `download_sems` setting in `config.json`, which sets the number of concurrent downloads per thread. Takes a whole number.
* **Default:** `None` (uses the value in `config.json`).
* **Available in:** The main program and `metadata` only.

### -dl, --download-limit \[argument]

* **Overrides:** The `download_limit` setting in `config.json`.
* **Limits:** Maximum download speed, shared across all downloads in the run, in bytes per second. Values below `1024` are raised to `1024`.
* **Accepts:** Human-readable sizes such as `10MB`.
* **Default:** No limit.
* **Available in:** The main program, `manual` and the check commands (not `metadata` or `db`).

### -ad, --allow-dupes (also `--allow-dupe-downloads`; turn off with `--no-allow-dupes`)

* **Sets:** Downloads media that appears in several posts once for each post, instead of once.
* **Default:** Off (the `ALLOW_DUPE_MEDIA` setting).
* **Available in:** Every mode: main, `metadata`, `manual` and the `*_check` commands.

***

## Download Cleanup

### -ar, --no-auto-resume

* **Effect:** Deletes temporary `.part` files instead of resuming them.
* **Default:** `false` (partial downloads are kept so they can resume).
* **Available in:** The main program, `manual` and the check commands (not `metadata` or `db`).
