# Placeholders

> ⚠️ **Rechecking files:** Run `--metadata-update` after updating your config if you want to recheck existing files.

<details>

<summary>Windows path warning</summary>

In JSON config files, backslashes (`\`) must be escaped as `\\` or replaced with `/`. Not doing this can cause an error.

```text
C:\Users\you\.config\ofscraper\bin\ffmpeg.exe  ->  C:\\Users\\you\\.config\\ofscraper\\bin\\ffmpeg.exe
C:\Users\you\.config\ofscraper\bin\ffmpeg.exe  ->  C:/Users/you/.config/ofscraper/bin/ffmpeg.exe
```

</details>

## Example of generated filenames

The placeholders below substitute the `{}` values in your config (see [Example Configs](../example-configs.md)):

```json
"file_options": {
    "save_location": "~/Data/ofscraper",
    "dir_format": "{model_username}/{responsetype}/{mediatype}/",
    "file_format": "{filename}.{ext}",
    "textlength": 0,
    "space_replacer": " ",
    "date": "MM-DD-YYYY",
    "text_type_default": "letter",
    "truncation_default": true
}
```

With this config, the generated path is:

```text
~/Data/ofscraper/{model_username}/{responsetype}/{mediatype}/{filename}.{ext}
```

***

> ℹ️ Placeholders are generally the same across the options on this page.

## dir\_path and filename

Every placeholder, with which template accepts it, is in [Placeholders](../../../reference/placeholders.md) in the Technical Reference. You can use placeholders without underscores (`_`), for example `{modelusername}`.

A few things worth knowing:

* `{original_filename}` is the filename as sent by OnlyFans (it may or may not include `source`). On Fansly it's the Fansly media ID.
* `{site_name}` is `Onlyfans` or `Fansly`.
* `{text}` file name truncation is tested to fit within OS limits, though setting a `textlength` limit is still advisable.
* `{root}` is the media root unless `dir_format` or `file_format` uses `{site_name}`. `{save_location}` is `<save location>/Fansly` on Fansly runs, even when `{site_name}` in `dir_format` or `file_format` drops that folder from the media path.

### dir\_path

The relative directory path within `save_location` where files are stored.

> ℹ️ No unique placeholders.

### filename

The file's name segment in the saved path. It can also use `{ext}`, the file extension.

> ℹ️ Include a unique element (such as `text`, `media_id`, `post_id`, or `filename`) to avoid naming conflicts.

***

## Text Placeholders

Text files are based on posts and have access to the same placeholders as other media, **except**:

* `media_id`
* `download_type`

Some placeholders behave differently for text files:

* `filename` is replaced with `text`
* `quality` is always `source`
* `media_type` is always `"Text"`

[Downloading Text Files](../../../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/selecting-posts/README.md#downloading-text-files)

***

## metadata

Controls where metadata is saved.

[Setting metadata path](../setting-metadata-path.md)

***

## response\_type placeholder

[Responsetype Placeholders](remapping-responsetype.md)
