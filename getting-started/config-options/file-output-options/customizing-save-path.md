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

> ℹ️ You can use placeholders without underscores (`_`).

| Placeholder | Meaning |
|---|---|
| `{response_type}` | `Posts`, `Messages`, `Archived`, `Stories`, `Profile`, `Streams` (paid content maps to `Messages` by default) |
| `{post_id}` | ID of the post |
| `{media_id}` | ID of the media |
| `{file_name}` | The filename; videos include the quality (e.g. `source`, `720`) |
| `{only_file_name}` | The filename without quality on videos |
| `{original_filename}` | Filename as sent by OnlyFans (may or may not include `source`; `None` when the media has no URL). On Fansly it's the Fansly media ID; for text files it's the cleaned-up post text. |
| `{media_type}` | `Images`, `Audios`, `Videos`, `Forced_skipped`, or `Text` (for text files) |
| `{quality}` | Quality of the media; non-videos are always `source` |
| `{value}` | Whether the content is categorised as `Paid` or `Free` |
| `{model_id}` | Unique ID number for the creator |
| `{first_letter}` | First letter of the creator's username |
| `{site_name}` | `Onlyfans` or `Fansly` |
| `{text}` | The post or message text. File name truncation is tested to fit within OS limits, though setting a `textlength` limit is still advisable. |
| `{date}` | The post date, formatted with the `date` config setting |
| `{model_username}` | The creator's username |
| `{username}` | The creator's username |
| `{profile}` | The currently active profile |
| `{my_username}` | The authorised account's username |
| `{my_id}` | The ID number for the authorised account |
| `{label}` | The label assigned to the post, or the text `None` when the post has no label |
| `{download_type}` | `Protected` or `Normal`, depending on whether decryption is needed |
| `{current_price}` | `Free` if the current price is 0 dollars, otherwise `Paid` (`Unknown_Price` when the creator's details aren't loaded) |
| `{regular_price}` | `Free` if the regular price is 0 dollars, otherwise `Paid` (`Unknown_Price` when the creator's details aren't loaded) |
| `{promo_price}` | `Free` if the promo price is 0 dollars, otherwise `Paid` (`Unknown_Price` when the creator's details aren't loaded) |
| `{renewal_price}` | `Free` if the renewal price is 0 dollars, otherwise `Paid` (`Unknown_Price` when the creator's details aren't loaded) |
| `{args}` | The passed arguments namespace; access keys with dot (`.`) syntax |
| `{config}` | The config dictionary; access keys with bracket (`[]`) syntax |
| `{modelObj}` | The creator data class; access properties with dot (`.`) syntax |
| `{config_path}` or `{configpath}` | Path to the current config directory |
| `{root}` | A `pathlib.Path` of `{save_location}`: the save location with the Fansly subfolder on Fansly runs. It is the media root unless `dir_format` or `file_format` uses `{site_name}`. |
| `{save_location}` | The configured save location. On Fansly runs it is `<save location>/Fansly`, even when `{site_name}` in `dir_format` or `file_format` drops that folder from the media path. |
| `{user_name}` | The creator's username, the same as `{model_username}` (alias: `{username}`) |

### dir\_path

The relative directory path within `save_location` where files are stored.

> ℹ️ No unique placeholders.

### filename

The file's name segment in the saved path.

> ℹ️ Include a unique element (such as `text`, `media_id`, `post_id`, or `filename`) to avoid naming conflicts.

| Placeholder | Meaning |
|---|---|
| `{ext}` | The file extension of the media |

***

## Text Placeholders

Text files are based on posts and have access to the same placeholders as other media, **except**:

* `media_id`
* `download_type`

Some placeholders behave differently for text files:

* `filename` is replaced with `text`
* `quality` is always `source`
* `media_type` is always `"Text"`

[Downloading Text Files](../../../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/selecting-posts/downloading-text-files.md)

***

## metadata

Controls where metadata is saved.

[Setting metadata path](../setting-metadata-path.md)

***

## response\_type placeholder

[Responsetype Placeholders](remapping-responsetype.md)
