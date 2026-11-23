---
description: Settings for File Names
---

# File Output Options

## Save Path Options

[Placeholders](customizing-save-path.md)

### save\_location

Root save folder.

### dir\_format

Format for directory paths.

### file\_format

Format for file names.

### textlength

Sets a cap on the `{text}` placeholder; `0` means no limit.

Whether the cap counts words or letters is set by `text_type_default`. The `--textlength` and `--text-type` arguments override both settings for one run.

### space\_replacer

> ℹ️ **Filename only:** This setting applies only to the filename and doesn't affect parent directories.

Replaces all spaces in the filename with this character. Use it together with the `{text}` placeholder.

### text\_type\_default

Whether `textlength` counts words or letters: `word` or `letter` (default `letter`).

* Applies unless `--text-type` is passed.
* In `word` mode, words are split on `space_replacer` (or a space), so the cap still works when `space_replacer` isn't a space.

### truncation\_default

* When `true`, text calculated to exceed the system path limit is shortened.
* Files whose paths still exceed the limit may fail.

### filename\_collision

> ℹ️ **Since 3.15.0.** This setting isn't in 3.14.7 and earlier. See [Fork Changes](../../../fork-changes.md).

Controls what happens when a download's path is already taken by a different file (for example, when `file_format` uses `{text}` and two posts have the same text):

* `media_id` (default): keep both. The new download is saved as `name_<media_id>` (then `name_<media_id>_2` and so on), and the database records the name it was actually saved under. If the existing file has identical content, it's reused instead of saving a copy.
* `overwrite`: the old behaviour. The larger of the two files is kept and the other is lost.
* Can also be set with the `OFSC_FILENAME_COLLISION_DEFAULT` environment variable.

To re-download media lost to collisions in older versions, see [Recover Filename Collisions](../../../using-the-scraper/recipes/recover-filename-collisions.md).

### date

The date syntax doesn't use bracket notation; it follows Arrow's format tokens. See [Arrow supported tokens](https://arrow.readthedocs.io/en/latest/guide.html#supported-tokens).

If you need additional help, open an issue in the repository.

***

## Other Related Options

These options also affect the final file name.

### responsetype

[Responsetype Placeholders](remapping-responsetype.md)

***

## metadata

[Setting metadata path](../setting-metadata-path.md)

Metadata is mainly used for:

* Duplicate checking
* Speeding up profile scans

It can also be shared with other programs via the `.db` files created.
