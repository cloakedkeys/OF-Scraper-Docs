---
description: Filter downloaded media by type, size, length, quality, date and order.
---

# Media Filters Options

## Media Type Filter

### -mt, --mediatype (also `--mediatypes`, `--media-types`, `--media-type`) \[argument]

* **Filters:** Media by type.
* **Possible choices:** `Audios`, `Videos`, `Images`.
* **Default:** `Audios`, `Videos`, `Images`.
* **Example:** `-mt Images` downloads images only.

***

## File Size Filters

### -sx, --size-max \[argument]

* **Filters:** Skips files larger than the given size.
* **Accepts:** Human-readable sizes such as `10MB` or `500GB`.
* **Default:** `None` (no maximum size filter).
* **Example:** `-sx 1GB` downloads only files 1 GB or smaller.

### -sm, --size-min \[argument]

* **Filters:** Skips files smaller than the given size.
* **Accepts:** Human-readable sizes such as `10MB` or `500GB`.
* **Default:** `None` (no minimum size filter).
* **Example:** `-sm 50MB` downloads only files 50 MB or larger.

### How the size limits work

* A file outside the limits is **skipped, not failed**, straight away with no retries. It isn't saved as downloaded, so it's tried again on the next run, for example after you change the limit.
* A DRM video is checked as a whole (audio and video together), not track by track. If one track is skipped, the whole video is.
* Files the server sends without a size get the limits and the skip script too.
* The after-download script gets size-skipped items as `skipped`.

> ℹ️ **Before 3.16.6, size-skipped files were saved as downloaded and never tried again.** The first start on 3.16.6 or later sets those rows back (files with no file on disk only, after making a backup).

***

## Media Length Filters (Video Only)

These filters apply only to video files.

### -lx, --length-max \[argument]

* **Filters:** Skips videos longer than the given duration.
* **Accepts:** A whole number of seconds (`0` or more), e.g. `90`.
* **Default:** `None` (no maximum length filter).
* **Example:** `-lx 30` downloads only videos 30 seconds or shorter.

### -lm, --length-min \[argument]

* **Filters:** Skips videos shorter than the given duration.
* **Accepts:** A whole number of seconds (`0` or more), e.g. `90`.
* **Default:** `None` (no minimum length filter).
* **Example:** `-lm 5` downloads only videos 5 seconds or longer.

***

## Media Quality Filter

### -q, --quality \[argument]

* **Sets:** The minimum acceptable video quality.
* **Possible choices:**
  * `source`: Tries to download the highest available quality (may not always be available).
  * `240`: Selects videos with a resolution of at least 240p.
  * `720`: Selects videos with a resolution of at least 720p.
* **Default:** `source`.
* **Note:** The program may download a higher quality version if the requested quality isn't available.

***

## Media ID Filter

### -mid, --media-id \[argument]

* **Filters:** Media by media ID.
* **Default:** `None`.
* **Note:** Doesn't speed up scanning, because filtering runs after all posts are fetched.

***

## Media Count and Order

### -mxc, --max-media-count \[argument]

* **Sets:** The maximum number of media items to process.
* **Default:** `0` (no limit).

### -mst, --media-sort \[argument]

* **Changes:** The media processing order before actions (for example, download).
* **Possible choices:** `random`, `text`, `date`, `filename`.
* **Default:** `None` (uses the default order for the action).
* **Note:** The check commands (`post_check`, `msg_check`, `paid_check`, `story_check`) accept a different list: `number`, `username`, `downloaded`, `unlocked`, `length`, `mediatype`, `post_date`, `post_media_count`, `responsetype`, `price`, `post_id`, `media_id`, `text`.

### -mdc, --media-desc

* **Sorts:** The media list in descending order.

***

## Download Scope and Dates

### -e, --force-all (also `--dupe`, `--dupe-all`)

* Downloads all found files regardless of database presence.
* **Default:** `False`.

### -eq, --force-model-unique (also `--dupe-model-unique`, `--dupe-model`)

* Downloads files only if not present for the current model.
* **Default:** `False`.

### -rd, --redownload (also `--re-download`)

* Forces scanning and redownloading of all files in the selected post types. Implies `--force-all`, `--after 2000` and a `--before` of tomorrow for the run.
* **Default:** `False`.

See [Valid date inputs](../../../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/selecting-posts/README.md#valid-inputs) for accepted date formats.

### -be, --before \[argument]

* Processes media from posts on or before the given date.
* **Accepts:** `MM/DD/YYYY`, `YYYY-MM-DD`, or a relative date such as `3 weeks ago`.

### -af, --after \[argument]

* Processes media from posts on or after the given date.
* **Accepts:** `MM/DD/YYYY`, `YYYY-MM-DD`, or a relative date such as `3 weeks ago`.

> ℹ️ **Fork:** a date that can't be read prints a short usage message instead of a traceback.
