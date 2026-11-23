# Downloading Content

## Contents

* [Selecting Posts](#selecting-posts)
* [Labels](#labels)
* [Downloading Text Files](#downloading-text-files)
* [Bypass dupe check](#bypass-dupe-check)
* [Filtering media](#filtering-media)
* [Filter Post by Date](#filter-post-by-date)
* [Filtering Timed Post (Promotional)](#filtering-timed-post-promotional)
* [Search entire paid page](#search-entire-paid-page)

## Selecting Posts

### By post type

Pass a comma-separated list of post areas to download:

```sh
ofscraper --action download --posts highlights,timeline
```

Or repeat `--posts`:

```sh
ofscraper --action download --posts highlights --posts timeline
```

Duplicates are removed automatically.

### Options

* `profile`
* `highlights`
* `timeline`
* `archived`
* `stories`
* `messages`
* `purchased`
* `pinned`
* `streams`
* `labels`

#### Special Options

* `all`: scrapes `highlights`, `timeline`, `archived`, `stories`, `pinned`, `purchased`, `messages`, `profile`, and `streams` (labels require `labels`, `labels+`, or `labels*`)
* `labels*` or `labels+`: scrapes `all` plus `labels`

#### remove post type

Exclude a post type by prepending a hyphen (`-`), such as `-pinned`. This removes any selection, including from `all`. Hyphen exclusions only work with `--posts`, not with `--like-area` or `--download-area`.

***

## Labels

Version 3.9 introduced a performance optimisation to `--posts all` by disabling label scans by default:

* In earlier versions, `--posts all` scanned labels to populate the `labels` table.
* While useful for some workflows, scanning labels can extend scan times if you don't need them in your database.
* Since version 3.9, labels are disabled by default with `--posts all`.

Add labels to `all`:

```sh
ofscraper --posts all,labels
```

Scrape just labels:

```sh
ofscraper --posts labels
```

Shorthands for all posts plus labels:

```sh
ofscraper --posts labels*
```

Or:

```sh
ofscraper --posts labels+
```

To add labels to `all` permanently, set the environment default `OFSC_INCLUDE_LABELS_ALL` to `True`.

On repeat runs, labels that have nothing new aren't paged through again. Check modes still scan labels in full.

***

## Downloading Text Files

> ℹ️ Text files are handled differently because there are no text media uploads; instead, they're based on posts and tied to multiple media.

There is no `config.json` setting for text files (`--mediatypes` / `-mt` and `config.json`'s `filter` only accept `Videos`, `Audios`, and `Images`). Use these command-line options instead:

* `--text` (also `-t`, `--download-text`): downloads text files alongside media.
* `--text-only` (also `-tx`, `--download-text-only`): downloads only text files and skips all media.

Notes:

* On the content-check and manual commands, `--text` and `--text-only` can't be used together, and their short forms are `-tn` (`--text`) and `-tp` (`--text-only`) instead of `-t` and `-tx`.
* Text files are only written by the `download` action, not by `like` or `unlike`.

***

## Bypass dupe check

By default, downloaded items are recorded in a database to prevent duplicate downloads. To download all available content for the current creator regardless, pass `--force-all`:

```sh
ofscraper --action download --force-all
```

* `--force-all` (`-e`, also `--dupe`, `--dupe-all`) downloads every file found, whatever the database says.
* `--force-model-unique` (`-eq`, also `--dupe-model-unique`, `--dupe-model`) downloads only files whose media ID isn't in the database for the current creator.
* `--redownload` (`-rd`, also `--re-download`) scans and downloads every file in the selected post types again. For the run it implies `--force-all`, `--after 2000` and a `--before` of tomorrow.
* Since 3.18.0, `--allow-dupes` (`-ad`, also `--allow-dupe-downloads`; turn it off with `--no-allow-dupes`) downloads media that appears in several posts once for each post, instead of once. It's off by default (the `ALLOW_DUPE_MEDIA` setting) and works in every mode: main, `metadata`, `manual` and the `*_check` commands.

***

## Filtering media

These filters work on the media found in the selected posts. The `config.json` versions are in [Media Filtering Options](../../../../getting-started/config-options/download-options/README.md#media-filtering-options).

| Option | What it keeps | Example |
|---|---|---|
| `--mediatype` (`-mt`) | `Audios`, `Videos` or `Images` (all three by default) | `-mt Images` downloads images only |
| `--size-max` (`-sx`) | Files at or below the size. Takes bytes or sizes such as `10MB` | `-sx 1GB` |
| `--size-min` (`-sm`) | Files at or above the size | `-sm 50MB` |
| `--length-max` (`-lx`) | Videos at or below the length, in whole seconds (`0` or more). Videos only | `-lx 30` |
| `--length-min` (`-lm`) | Videos at or above the length | `-lm 5` |
| `--quality` (`-q`) | The lowest video quality to accept: `240`, `720` or `source` (the default). The smallest available quality at or above it is downloaded, or `source` when none matches | `-q 720` |
| `--media-id` (`-mid`) | Only the given media IDs. It doesn't speed up scanning, because filtering runs after all posts are fetched | |
| `--max-media-count` (`-mxc`) | At most this many media items (`0`, the default, means no limit) | |

`--media-sort` (`-mst`) changes the order media is processed in before actions such as download: `random`, `text`, `date` or `filename`. Add `--media-desc` (`-mdc`) for descending order.

### How the size limits work

* A file outside the limits is **skipped, not failed**, straight away with no retries. It isn't saved as downloaded, so it's tried again on the next run, for example after you change the limit.
* A DRM video is checked as a whole (audio and video together), not track by track. If one track is skipped, the whole video is.
* Files the server sends without a size get the limits and the skip script too.
* The after-download script gets size-skipped items as `skipped`.

> ℹ️ **Before 3.16.6, size-skipped files were saved as downloaded and never tried again.** The first start on 3.16.6 or later sets those rows back (files with no file on disk only, after making a backup).

***

## Filter Post by Date

> ℹ️ `X` must be a valid date.

### Before

Filters posts on or before the specified date. Works for downloading, liking, and unliking posts:

```sh
ofscraper --action download --before X
```

### After

Filters posts on or after the specified date. Works for downloading, liking, and unliking posts:

```sh
ofscraper --action download --after X
```

### **Valid Inputs**

> ℹ️ See the Arrow documentation for all supported input formats.

`YYYY-MM-DD, YYYY-M-DD, YYYY-M-D, YYYY/MM/DD, YYYY/M/DD, YYYY/M/D, YYYY.MM.DD, YYYY.M.DD, YYYY.M.D, YYYYMMDD, YYYY-DDDD, YYYYDDDD, YYYY-MM, YYYY/MM, YYYY.MM, YYYY, MM/DD/YYYY, M/D/YYYY`

`MM/DD/YYYY` and `M/D/YYYY` are accepted after the ISO formats, and the command-line help shows `MM/DD/YYYY` as the main format.

### Dehumanize Strings

Relative strings can be converted into dates using the form `<number> <timeframe> ago`.

**Timeframes:**

* `year`
* `month`
* `week`
* `day`
* `hour`
* `minute`
* `second`

Combine multiple timeframes with a comma for finer precision (when using debuggers, output displays in UTC):

```text
1 year ago, 1 month ago
```

***

## Filtering Timed Post (Promotional)

Skip all timed posts:

```sh
ofscraper --action download --skip-timed
```

### Filtering by text content

Accepts regex patterns (enclose the pattern in quotes to escape it properly). Including a capital letter enables case-sensitive matching.

#### Filter

Include only posts matching the regex pattern:

```sh
ofscraper --action download --filter X
```

#### Neg Filter:

Exclude posts matching the regex pattern (`--neg-filter` or `-nf`):

```sh
ofscraper --action download --neg-filter X
```

### Other post filters

| Option | What it does |
|---|---|
| `--skip-timed` (`-sk`) / `--only-timed` (`-ok`) | Skip, or keep only, temporary posts (mostly promotions). Pick one. |
| `--mass-skip` (`-ms`) / `--mass-only` (`-mm`) | Skip, or keep only, mass messages. Pick one. |
| `--protected-only` (`-to`) / `--normal-only` (`-no`) | Keep only content that needs decryption, or only content that doesn't. |
| `--label` (`-lb`) | Keep only content with the given labels. |
| `--post-id` (`-pd`) | Keep only the given post IDs: one or more, separated by commas, or URLs containing a post ID. For timeline and message posts, fewer than 10 IDs are looked up directly. To process posts from several creators, use [manual mode](../../../scraping-individual-posts-or-media.md). |
| `--block-ads` (`-ba`) | Drop posts matching the built-in ad regex (the same as the `block_ads` setting in [Media Filtering Options](../../../../getting-started/config-options/download-options/README.md#block_ads)). Main program only. |
| `--max-post-count` (`-xc`) | At most this many media items per creator, the same setting as `--max-media-count` (`0` means no limit; default `max_post_count` from `config.json`). |
| `--post-sort` (`-pst`), `--post-desc` (`-pdc`) | Order posts before actions such as `like` or `unlike`: `date` (the default), and descending with `--post-desc`. |

***

## Search entire paid page

### Downloading Purchases From Deleted Models

`--scrape-paid` scrapes your entire paid page. It's meant for creators whose accounts are deleted. The regular scraper already covers content from creators with active accounts.

Paid content is the only type of content that can be scraped for deleted creators.

For example:

```sh
ofscraper --action download --scrape-paid
```

To scrape only the paid page and skip other prompts:

```sh
ofscraper --scrape-paid
```
