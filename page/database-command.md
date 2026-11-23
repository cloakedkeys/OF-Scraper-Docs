---
description: Print or export what the database holds, without contacting the site
---

# Database Command

`ofscraper db` reads the media rows in each selected creator's `user_data.db` and prints them as a table. It makes no API calls for the media itself.

```sh
ofscraper db --usernames creatorname
```

## Choosing rows

It takes the usual options:

* **Creators:** `-u` and the other user selection options.
* **Areas:** `-o`, for example `-o messages,purchased`.
* **Media filters:** type, size, length, downloaded, locked, preview, protected and dates.
* **`--post-id` and `--media-id`:** one id, or several separated by commas or spaces.
* **Order and limit:** `--db-sort`, `--db-asc` and a hard limit.

See [Command-line options](../reference/cli.md#db) for the full list.

## Exporting

`-ep PATH` or `--export PATH` also writes the rows to a `.csv`. With several creators, every creator's rows go into the one file.

## What it changes

Nothing, unless you pass `--unmark-permanent-skips`.

* Databases are opened read-only, so it works on read-only files and network shares (`\\server\share`).
* A creator with no database is skipped with a short message. No empty file or folder is created.
* A database it can't read is named and skipped, and the other creators still show.
* Databases from older versions, missing newer columns, work.
* Over all areas, a database that holds several creators shows only the chosen creator's media.

### Undoing permanent skips

`--unmark-permanent-skips` keeps only the rows that the [skip download script](../getting-started/config-options/script-options.md#skip-download-script-skip_download_script) skipped for good, prints them, and sets them back to not downloaded. The next normal run asks the script about them again. Narrow it with the creator options, `--post-id` or `--media-id`.

* Real downloads are never touched.
* A media's download state is kept on all of its rows, so its rows in other posts change too.

> ℹ️ **Fork:** the read-only behaviour, the working `--post-id` and `--media-id`, and `--unmark-permanent-skips` came in 3.16.6. See [Fork Changes](../fork-changes.md).
