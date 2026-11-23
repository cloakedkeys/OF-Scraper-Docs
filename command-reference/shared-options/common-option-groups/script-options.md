---
description: Run custom scripts at key points during a scrape or download.
---

# Script Options

See [Script Options](../../../getting-started/config-options/script-options.md) for how scripts receive input and what they return.

These options are available in the main program, `manual` and the check commands (not `metadata` or `db`).

### -aas, --after-action-script \[argument]

**Executes:** A custom script after an action finishes for a model.

**Runs:**

* After each model is downloaded in the main scraper.
* After each model's metadata is processed in metadata mode.
* After each model is processed in manual mode.
* For each unique model, after the current cart is downloaded in check mode.

### -ps, --post-script \[argument]

**Executes:** A custom script once the run finishes an action.

**Runs:**

* Once all models are downloaded or liked in scrape mode.
* Once all posts in manual mode are completed.
* After the current cart downloads finish in check mode, and after the download script runs for each user.
* After all metadata for all users is processed in metadata mode.

### -ns, --naming-script \[argument]

**Executes:** A script that generates the final filename dynamically.

**Runs:**

* When the temporary `.part` filename is generated for a download.
* When the final filename is generated for a media download.
* When the final filename is generated for a text download.

### -sdl, --skip-download-script \[argument]

**Executes:** A script that decides whether to skip or continue a download.

**Runs:**

* Just before a download starts.

### --retry-permanent-skips

**Effect:** Asks the skip download script again about files it skipped for good (`skip-permanent`) for the creators in this run.

**Available in:** The main program, `manual` and the `*_check` commands.

### -adl, --after-download-script \[argument]

**Executes:** A script that runs after a download finishes.

**Runs:**

* After a download completes.

