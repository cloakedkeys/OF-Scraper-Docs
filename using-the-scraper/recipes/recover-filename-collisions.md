---
description: Re-download media lost when two downloads were saved under the same file name
---

# Recover Filename Collisions

> ℹ️ **Since 3.15.0.** Not in 3.14.7 and earlier. See [Fork Changes](../../fork-changes.md).

## Background

The full recipe is also in [COLLISION_RECOVERY.md](https://github.com/cloakedkeys/OF-Scraper-Community/blob/main/COLLISION_RECOVERY.md).

A file name template can give different media the same name, for example one built on `{text}` or `{model_username}`. Before the fix, the second download replaced the first (the larger file was kept), but both were recorded as downloaded. The run reported both, yet only one file was left.

Current versions prevent this. If a different file already has the name, the download is saved as `name_<media_id>` (then `name_<media_id>_2` and so on), and the database records the name each file was actually saved under. An identical file already at that name is reused instead. To keep the old behaviour, set [`filename_collision`](../../getting-started/config-options/file-output-options/README.md#filename_collision) to `overwrite`.

Files already overwritten by older versions can't be brought back from disk. The command below finds media that were probably lost and marks them as not downloaded, so a normal run downloads them again.

## Preview

Stop the scraper first. The command works offline: it doesn't contact OnlyFans or change any media files. Run it on one creator's database:

```sh
python -m ofscraper.commands.recover_collisions "<profile>/.data/<model_id>/user_data.db"
```

The JSON report lists paths shared by different media and `media_to_mark`:

* These are **suspected** losses: old records can't show which media owns the file that survived, so every media in a shared group is included, even if some really had identical content.
* Several posts pointing at the same media isn't a collision on its own.
* Missing files that weren't shared are outside this command's scope.

## Apply

Run the same command with `--apply`:

```sh
python -m ofscraper.commands.recover_collisions "<profile>/.data/<model_id>/user_data.db" --apply
```

* Rechecks the database, writes a small JSON undo file beside it, and sets only `downloaded = 0` for the affected media (including their other post records).
* File names, hashes, sizes, and media files are left alone.
* The report gives the `undo_file` path.
* Running recovery again before re-downloading changes nothing and writes no new undo file.

## Re-download

Run a normal download for the affected creator and content areas, with `--after 2000` so old messages are included:

```sh
ofscraper --action download -u <creator> --posts all --after 2000
```

* **Don't use `--force-all`.** The cleared flags already make the affected media eligible, while media that weren't affected stay skipped.
* **Don't run `metadata ... update` between recovery and the download.** It can mark the shared paths as downloaded again.
* Normal access and content filters still apply. Media no longer available on OnlyFans can't be recovered.

## Undo

To reverse the flag reset **before downloading anything**, preview and then apply the undo file:

```sh
# Preview undo
python -m ofscraper.commands.recover_collisions "<database>" --undo "<undo-file.json>"

# Apply undo
python -m ofscraper.commands.recover_collisions "<database>" --undo "<undo-file.json>" --apply
```

Undo only restores the recorded rows whose flags are still `0`. It refuses a different database, and leaves other rows and columns untouched. Keep the undo file until you're happy with the result; it isn't a general database backup.

## Limitations

* Only the database you name is scanned. Collisions between different creators' databases aren't detected.
* Existing files are grouped by filesystem identity, including case variants on case-insensitive storage. Missing files are grouped only by exact path, so missing case variants can't be matched.
* If recorded paths are relative, pass `--path-root` with the working directory used for the original downloads.
* Use it as a one-off repair on databases from affected versions, not as routine maintenance: legitimate identical downloads can also share a path.
