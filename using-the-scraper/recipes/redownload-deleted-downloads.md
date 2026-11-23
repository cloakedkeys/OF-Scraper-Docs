# Redownload Deleted Downloads

## With metadata (recommended)

> ⚠️ **Use the exact same settings for both steps** so the same posts are affected.

1. **Run `ofscraper metadata --metadata update`** (short form: `-md update`), with the same filters as your download:

   ```sh
   ofscraper metadata --metadata update
   ```

   * Marks downloads and filenames from the files on disk, then refreshes metadata from the site.
   * Much faster than `--force-all` (also `--dupe`), since no files are written to disk and fewer requests are needed.
   * Add extra arguments if needed, for example `--after 2000`.

2. **Download normally:**

   * Any files now marked as missing are re-downloaded.

## Force all downloads

```sh
ofscraper --force-all
```

Forces all downloads to be processed.
