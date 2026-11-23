# Metadata Check Mode Options

> ℹ️ **Metadata mode inherits most options from the main scraper, with a few removed because they don't apply outside downloading.**

> ℹ️ **Without `--force-all` or `--force-model-unique`, media is filtered to only items marked as not downloaded in the database.**

## Syntax

```
ofscraper metadata [options]
```

### Example

```
ofscraper metadata --metadata check
```

## General Options

* [General Program Options](shared-options/common-option-groups/)
* [Shared Scrape and Metadata Check Mode Options](shared-options/scrape-metadata-options/)

## Options

### -md, --metadata \[argument]

Sets how metadata mode updates the database.

**Available modes:**

* **`check`:** Updates metadata fields for the selected area via the API. Doesn't check for new filenames.
* **`update`:** Performs two actions:
  1. Updates download status and filenames based on whether the files exist on disk.
  2. Updates metadata fields for the selected area via the API.
* **`complete`:** Marks downloads as complete and updates metadata fields via the API. Also uses a new filename if one is available.

### -ms, --mark-stray-locked (also `--mark-stray`)

Marks unmatched media items as locked.

**Details:**

* Targets media items in the `--after` / `--before` date range that can no longer be retrieved from the API (for example, after deletion).
* Excludes media items with labels.
* Applied per API type: Timeline, Archived Posts and Messages.
* Has no effect if `--scrape-paid` is the only argument.

**Use case:** Marking unretrievable items as locked stops the main scraper from using them to set the minimum date.

### -an, --anon

Uses anonymous credentials. Requires `--usernames` with a name other than `ALL`, forces `--individual` search and removes `--list`. Most media is ignored.

***

### -sp, --scrape-paid \[argument]

Sets how metadata mode updates the database for `--scrape-paid` content.

**Fork:** models named with `--excluded-username` are skipped. See [`--excluded-username`](shared-options/scrape-metadata-options/user-selection-options.md).

Accepts the same modes as `--metadata`:

* **`check`:** Updates metadata fields for the selected area via the API. Doesn't check for new filenames.
* **`update`:** Performs two actions:
  1. Updates download status and filenames based on whether the files exist on disk.
  2. Updates metadata fields for the selected area via the API.
* **`complete`:** Marks downloads as complete and updates metadata fields via the API. Also uses a new filename if one is available.
