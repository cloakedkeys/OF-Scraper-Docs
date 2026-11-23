# Script Options

See [Scripts](../../using-the-scraper/recipes/scripts.md) for examples.

## Contents

* [After Action Script (`after_action_script`)](#after-action-script-after_action_script)
* [Post Script (`post_script`)](#post-script-post_script)
* [Naming Script (`naming_script`)](#naming-script-naming_script)
* [After Download Script (`after_download_script`)](#after-download-script-after_download_script)
* [Skip Download Script (`skip_download_script`)](#skip-download-script-skip_download_script)
* [How scripts run](#how-scripts-run)

## After Action Script (`after_action_script`)

Runs after an action for a creator completes. Configure with `--after-action-script` or `after_action_script` in `config.json`.

### **Trigger Conditions**

* After each creator is downloaded in the main scraper (including daemon mode).
* After each creator's like/unlike process finishes (including daemon mode).
* After each creator's metadata is processed in metadata mode.
* After each creator is processed in manual mode.
* For each unique creator, after the current cart is downloaded in check mode.
* For each creator after `scrape_paid` is processed (`modeldeleted` or creators without an active account are run together as one unit).

### **Data Sent**

Sent as a JSON dictionary via standard input (`stdin`):

| Key | Description |
|---|---|
| `username` | Creator's username (string) |
| `action` | Action run (string) |
| `model_id` | Creator's ID (integer) |
| `media` | Media dictionary from API; each item includes `filepath`, `download_status` (`succeeded`, `failed`, or `skipped`), `size`, and `metadata_status` (`skipped`, `failed`, `changed`, or `unchanged`) |
| `posts` | Posts dictionary from API |
| `userdata` | Dictionary from the users API |

***

## Post Script (`post_script`)

Runs after all actions for all creators complete. Configure with `--post-script` or `post_script` in `config.json`.

### **Trigger Conditions**

* Once all creators are downloaded or liked in scrape mode.
* After each cycle in daemon mode.
* Once all posts from manual mode are completed.
* After the current cart downloads are processed in check mode, and after `after_action_script` has run for each creator.
* After all metadata for all creators is processed in metadata mode.

### **Data Sent**

Sent as a JSON dictionary via standard input (`stdin`):

| Key | Description |
|---|---|
| `like_processed_users` | Creators who completed the `like` action |
| `like_unprocessed_users` | Creators queued for `like` who weren't processed |
| `unlike_processed_users` | Creators who completed the `unlike` action |
| `unlike_unprocessed_users` | Creators queued for `unlike` who weren't processed |
| `download_processed_users` | Creators whose content was downloaded |
| `download_unprocessed_users` | Creators queued for download who weren't processed |
| `scrape_paid_processed_users` | Creators processed during `scrape_paid` |
| `scrape_paid_unprocessed_users` | Creators queued for `scrape_paid` who weren't processed |

***

## Naming Script (`naming_script`)

Dynamically generates the final filename or full path for a downloaded media item. Configure with `--naming-script` or `naming_script` in `config.json`.

### **Trigger Conditions**

* Runs for each media item while its temporary filename is being generated.
* Runs again after the temporary file is downloaded and before it is renamed to its final path.
* **Special case:** also runs before generating filenames for text files when using `--text` or `--text-only`.

### **Data Sent**

Sent as a JSON dictionary via standard input (`stdin`):

| Key | Description |
|---|---|
| `media` | Dictionary representing the media item |
| `post` | Dictionary representing the associated post |
| `dir` | Calculated directory path (string) |
| `file` | Calculated filename (string) |
| `dir_format` | Current `dir_format` setting (string from config) |
| `file_format` | Current `file_format` setting (string from config) |
| `metadata` | Current `metadata` format setting (string from config) |
| `username` | Creator's username (string) |
| `model_id` | Creator's ID (integer) |
| `post_id` | Associated post ID (integer) |
| `media_id` | Media item ID (integer) |
| `media_type` | Type of media |
| `value` | Value associated with the media |
| `date` | Formatted date for the media/post (string) |
| `response_type` | Response type of the media (string) |
| `label` | String representing associated labels |
| `download_type` | Type of download |

For text files, `media`, `media_id`, `media_type`, and `download_type` are `null`; `label` is the text `None` when there's no label; and `value` is capitalised.

### **Expected Output**

Print the **full desired path** to standard output (`stdout`). OF-Scraper uses this output to rename or move the downloaded file.

***

## After Download Script (`after_download_script`)

Runs after a download completes. Configure with `--after-download-script` or `after_download_script` in `config.json`.

### **Trigger Conditions**

* Runs after a download completes successfully.

### **Data Sent**

A single string: the final filepath of the download.

***

## Skip Download Script (`skip_download_script`)

Determines whether to skip or continue a download. Configure with `--skip-download-script` or `skip_download_script` in `config.json`.

### **Trigger Conditions**

* Runs before the download starts for each individual media item.
* Asked once per file per run. For a DRM video it's asked per track, and if it skips one track the whole video is skipped.

### **Data Sent**

Sent as a JSON dictionary via standard input (`stdin`):

| Key | Description |
|---|---|
| `username` | Creator's username (string) |
| `model_id` | Creator's ID (integer) |
| `post_id` | Associated post ID (integer) |
| `media_id` | Media item ID (integer) |
| `media` | Dictionary representing the media item |
| `post` | Dictionary representing the associated post |
| `total_size` | Total size of the download in bytes (integer) |

### **Expected Output**

Return a string via standard output (`stdout`):

| Output | What happens |
|---|---|
| `false` (any case) or nothing | The file is **skipped for this run only**. It's counted as skipped, not saved as downloaded, and the script is asked about it again on the next run. |
| `skip-permanent` (any case) | The file is **skipped for good**. It's saved as downloaded with no file, and the script isn't asked about it again. |
| Anything else, or the script fails | The download **proceeds**. |

> ℹ️ **Before 3.16.6, `false` and nothing also saved the file as downloaded, so it was never asked about again.** To keep that behaviour, print `skip-permanent`.

### **Undoing permanent skips**

* `--retry-permanent-skips` on a normal run asks the script again about the files it skipped for good, for the creators in that run.
* `ofscraper db --unmark-permanent-skips` un-marks them without running a download. Narrow it with the creator options, `--post-id`, or `--media-id`. Only permanent skips are touched; real downloads stay marked.

***

## How scripts run

* **UTF-8 (all scripts):** Python scripts run in Python's UTF-8 mode, and output is read as UTF-8, so non-English names come through intact on Windows.

The naming, skip-download, and after-download scripts also behave like this:

* **The answer is used as soon as the script exits,** even if it started a program that keeps running in the background. OF-Scraper waits a moment for the rest of the output, then logs a warning.
* **Programs the script starts are stopped** once it exits, times out, or is cancelled, and when OF-Scraper exits. `nohup` and `&` don't keep a program running. On Linux and macOS, a program started in its own session (for example with `setsid`) is left running; on Windows, none is.
