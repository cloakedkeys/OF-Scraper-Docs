---
description: Select which post areas to scrape and how to filter and sort posts.
---

# Content Options

## Targeting Content

### -o, --posts \[argument]

* Selects which content areas to target for actions (`like`, `unlike`, `download`).
* **Possible choices:** `highlights`, `all`, `archived`, `messages`, `timeline`, `pinned`, `streams`, `stories`, `purchased`, `profile`, `labels`, `labels+`, `labels*`.
* `all` doesn't include labels. To include them, use `all,labels` or tags like `labels+` or `labels*`.
* **Default:** `None`.

### -t, --text (also `--download-text`)

* Downloads text files alongside media.
* **Note:** Affects only the `download` action.
* **Default:** `False`.

### -tx, --text-only (also `--download-text-only`)

* Downloads only text files, skipping all media. Also turns on `--text`.
* **Default:** `False`.

### -la, --like-area \[argument]

* Sets the area for `like` and `unlike` actions (overrides `--posts`).
* **Possible choices:** `all`, `archived`, `timeline`, `pinned`, `labels`, `streams`.
* **Default:** `None`.

### -da, --download-area \[argument]

* Sets the area for `download` actions (overrides `--posts`).
* **Possible choices:** `highlights`, `all`, `archived`, `messages`, `timeline`, `pinned`, `stories`, `purchased`, `profile`, `streams`, `labels`, `labels+`, `labels*`.
* **Default:** `None`.

***

## Filtering Content

### -sk, --skip-timed

* Skips temporary posts (commonly used for promotions).

### -ms, --mass-skip

* Excludes downloads marked as mass messages.

### -mm, --mass-only

* Includes only downloads labelled as mass messages.

### -ok, --only-timed

* Downloads only temporary posts (mostly used for promotions).

> ℹ️ Select only one of each pair: `--only-timed` or `--skip-timed`, `--mass-only` or `--mass-skip`.

### -ft, --filter \[argument]

* Includes only posts matching a regular expression.
* Case-sensitive if uppercase characters are included.
* **Default:** `".*"` (matches all posts).

### -nf, --neg-filter \[argument]

* Excludes posts matching a regular expression.
* Case-sensitive if uppercase characters are included.
* **Default:** `None` (no exclusion).

### -to, --protected-only

* Restricts downloads to content that requires decryption.

### -no, --normal-only

* Restricts downloads to content that doesn't require decryption.

### -lb, --label

* Scrapes content with specific labels.
* **Default:** `None` (no specific label).

### -pd, --post-id \[argument]

* Filters content by post ID.
* **Arguments:** One or more comma-separated (`,`) post IDs, or URLs containing a valid post ID.
* **Default:** `None`.
* **Note:** In certain situations this enables direct lookup, namely for timeline and message posts when fewer than 10 IDs are given.
* **Note:** Use `manual` mode if you want to process posts for multiple users.

***

## AD Filter

### -ba, --block-ads

* Filters posts with a regex to block posts containing common advertisement words.
* Works in the main program. Also applies when `block_ads` is turned on in `config.json`.
* **Default:** `None`.
* **Regex** (passed as a raw Python string):

```python
"(#(?:ad|ads|AD|advertising|sponsored|promotion)|trial|giveaway|\Buser\s+promo|shoutout|endorsement)"
```

***

## Date Range

`--before` and `--after` are Media Filters options. See [Media Filters Options](../common-option-groups/media-filters-options.md).

***

## Other Options

### -sp, --scrape-paid

* Scrapes the entire paid page for content (can be time-consuming).
* In `metadata` it takes a mode (`check`, `update` or `complete`), like `--metadata`.
* **Default:** `False`.
* **Fork:** `--excluded-username` skips the named models during this scan. See [`--excluded-username`](user-selection-options.md).

### -pst, --post-sort \[argument]

* Changes the post processing order before actions (for example, `like` or `unlike`).
* **Possible choices:** `date`.
* **Default:** `date`.

### -pdc, --post-desc

* Sorts the post list in descending order (for example, `like` or `unlike`).
* **Default:** `False`.

### -xc, --max-post-count \[argument]

* Sets the maximum number of posts to process.
* **Default:** `0` (no limit), or `max_post_count` from `config.json`.
