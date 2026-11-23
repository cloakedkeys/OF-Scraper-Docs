# Setting metadata path

In `config.json`, you can change the default metadata location or adjust where OF-Scraper looks for database files.

Using your existing metadata files from DIGITALCRIMINALS' script lets the duplicate checker work right away, and new entries are appended to the existing files.

***

## Config File Location

[Config Location](config-location.md)

## Changing metadata location

Update the `metadata` setting in `config.json` using any of these placeholders:

| Placeholder | Meaning |
|---|---|
| `{site_name}` (or `{sitename}`) | `Onlyfans` or `Fansly` (with that exact casing) |
| `{first_letter}` | First letter of the creator's username |
| `{model_username}` | The creator's username |
| `{username}` | The creator's username |
| `{model_id}` (or `{modelid}`) | Unique ID number for the creator |
| `{config_path}` (or `{configpath}`) | The config home folder (containing `config.json`); usually written `{configpath}` |
| `{profile}` | The currently active profile |
| `{save_location}` (or `{savelocation}`) | The parsed path specified in `save_location` (`<save location>/Fansly` on Fansly runs) |
| `{root}` | A `pathlib.Path` of `{save_location}` (`<save location>/Fansly` on Fansly runs) |
| `{my_username}` | The authorised account's username |
| `{my_id}` | The ID number assigned to the authorised account |

On Fansly runs, a site subfolder is added automatically if the `metadata` template uses none of `save_location`, `root`, `site_name`, or `model_id` (or their aliases).

> ⚠️ **No price placeholders in `metadata`:** `{current_price}`, `{regular_price}`, `{promo_price}`, and `{renewal_price}` are for file and folder names, not the metadata path. Using them in `metadata` makes the scraper fail. See [Placeholders](../../reference/placeholders.md).
