# Download Toggles

## auto\_resume

> ℹ️ Replaces `partfileclean`.

When set to `false`, OF-Scraper deletes `.part` files and can't auto-resume interrupted downloads.

***

## system\_free\_min

> ℹ️ Set to `0` to disable.

Stops scraping further post areas (`"Space min has been reached"`) once free space drops below the limit. Accepts bytes or a size string such as `10GB`. Space is measured on `OFSC_DISK_SPACE_CHECK_PATH` (default `/`), not `save_location`.

Checked:

* Before scraping
* Before each download starts

***

## verify\_all\_integrity

Default `false`. When `true`, ordinary video and audio downloads and Fansly streams are checked with `ffprobe` against the expected duration, and any truncated file is deleted and reported as failed. Requires `ffprobe`.
