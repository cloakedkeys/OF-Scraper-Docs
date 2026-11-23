---
description: Settings that control how and which media is downloaded
---

# Download Options

`downloadbars` and `temp_dir` are in [Advanced config options](../options/advanced-config-options.md).

## Download Toggles

### auto\_resume

> ℹ️ Replaces `partfileclean`.

When set to `false`, OF-Scraper deletes `.part` files and can't auto-resume interrupted downloads.

### system\_free\_min

> ℹ️ Set to `0` to disable.

Stops scraping further post areas (`"Space min has been reached"`) once free space drops below the limit. Accepts bytes or a size string such as `10GB`. Space is measured on `OFSC_DISK_SPACE_CHECK_PATH` (default `/`), not `save_location`.

Checked:

* Before scraping
* Before each download starts

### verify\_all\_integrity

Default `false`. When `true`, ordinary video and audio downloads and Fansly streams are checked with `ffprobe` against the expected duration, and any truncated file is deleted and reported as failed. Requires `ffprobe`.

***

## Media Filtering Options

These settings control which media is downloaded.

### filter

Controls which media types to download. Valid values: `Images`, `Audios`, `Videos` (case-insensitive).

### file\_size\_max

Sets the maximum file size allowed for downloads. (Older configs called this `file_size_limit`; it is still read.)

* Ignored if `0` or `None`.
* Value can be in bytes or a human-readable string like `"10MB"`.

### file\_size\_min

Sets the minimum file size allowed for downloads.

* Ignored if `0` or `None`.
* Value can be in bytes or a human-readable string like `"10MB"`.

See [How the size limits work](../../../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/selecting-posts/README.md#how-the-size-limits-work) for what happens to a file outside the limits.

### length\_max

Filters out videos longer than the given length (in seconds).

* Ignored if `0`.
* Applies only to videos.

### length\_min

Filters out videos shorter than the given length (in seconds).

* Ignored if `0`.
* Applies only to videos.

### block\_ads

Removes posts matching the built-in ad regex:

```python
r"(#(?:ad|ads|AD|advertising|sponsored|promotion)|trial|giveaway|\Buser\s+promo|shoutout|endorsement)"
```

### max\_post\_count

The maximum number of media items (not posts) to process per creator. `0` means no cap.
