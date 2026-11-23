---
description: Settings that control which media is downloaded
---

# Media Filtering Options

## filter

Controls which media types to download. Valid values: `Images`, `Audios`, `Videos` (case-insensitive).

## file\_size\_max

Sets the maximum file size allowed for downloads. (Older configs called this `file_size_limit`; it is still read.)

* Ignored if `0` or `None`.
* Value can be in bytes or a human-readable string like `"10MB"`.

## file\_size\_min

Sets the minimum file size allowed for downloads.

* Ignored if `0` or `None`.
* Value can be in bytes or a human-readable string like `"10MB"`.

## length\_max

Filters out videos longer than the given length (in seconds).

* Ignored if `0`.
* Applies only to videos.

## length\_min

Filters out videos shorter than the given length (in seconds).

* Ignored if `0`.
* Applies only to videos.

## block\_ads

Removes posts matching the built-in ad regex:

```python
r"(#(?:ad|ads|AD|advertising|sponsored|promotion)|trial|giveaway|\Buser\s+promo|shoutout|endorsement)"
```

## max\_post\_count

The maximum number of media items (not posts) to process per creator. `0` means no cap.
