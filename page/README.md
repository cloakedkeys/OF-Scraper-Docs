# Metadata

Metadata is automatically created when you download data. The tables and their structure are determined by the API you're using and the version of OF-Scraper you're running.

***

## Metadata location

Each creator has one `user_data.db` in the folder set by the `metadata` config value. The default is `{configpath}/{profile}/.data/{model_id}`, for example `~/.config/ofscraper/main_profile/.data/<model_id>/user_data.db`. To change it, see [Setting metadata path](../getting-started/config-options/setting-metadata-path.md).

Backups are kept in a `backup` folder beside the database.

Fansly runs use a separate `Fansly` subfolder when the template has no site-specific field, so Fansly rows do not land in the OnlyFans file.

***

## Schema

Every table and column is listed in [Database tables](../reference/database.md) in the Technical Reference.

The schema may be extended in future versions, but existing columns will remain for backwards compatibility.

Table rebuilds during migration and the Merge Databases menu keep every row, including `is_deleted`. A rebuild runs in one transaction, so if it fails the old table is left intact.

***

## Creating Metadata

### metadata mode

> ℹ️ You can use `--anon` to gather metadata without logging in, though you lose access to most media data.

Enter metadata mode with the `metadata` subcommand:

```sh
ofscraper metadata [args]
```

For example:

```sh
ofscraper metadata --metadata check
```

This updates metadata without downloading files. Existing stories are updated too, not just new ones, and messages keep their deleted flag.

Metadata mode and the main scraper share many command-line options: the main scraper downloads content, while metadata mode uses the API to fetch and update profile and content records in the database. Metadata mode accepts most of the main scraper's options, minus a few that only matter when downloading. Without `--force-all` or `--force-model-unique`, it works only on media the database marks as not downloaded.

### Metadata mode options

`--metadata` (`-md`) sets how the database is updated:

| Mode | What it does |
|---|---|
| `check` | Updates metadata fields for the selected area via the API. Doesn't check for new filenames. |
| `update` | First updates download status and filenames from whether the files exist on disk, then updates metadata fields via the API. |
| `complete` | Marks downloads as complete and updates metadata fields via the API. Also uses a new filename if one is available. |

* **`--scrape-paid` (`-sp`)** takes the same modes, for the paid content. Models named with `--excluded-username` are skipped. See [Exclude specific models](../using-the-scraper/batch-scraping-and-bot-actions/model-selection-sorting/README.md#exclude-specific-models).
* **`--mark-stray-locked` (`-ms`, also `--mark-stray`)** marks media in the `--after` / `--before` range that the API no longer returns (for example, after deletion) as locked. It skips media with labels, runs per API type (Timeline, Archived Posts and Messages), and has no effect if `--scrape-paid` is the only area. Marking them as locked stops the main scraper from using them to set the minimum date.
* **`--anon` (`-an`)** uses anonymous credentials. It needs `--usernames` with a name other than `ALL`, forces the individual username search and drops `--list`. Most media is ignored.

The full list is in [Command-line options](../reference/cli.md#metadata).
