# Table Management

## Contents

* [Tabs](#tabs)
* [Columns](#columns)
* [Picking media (the cart)](#picking-media-the-cart)
* [Downloading](#downloading)
* [Opening the download folder](#opening-the-download-folder)
* [Sorting the table](#sorting-the-table)
* [Filtering of the table](#filtering-of-the-table)

## Tabs

* **DataTable:** every media item, a page at a time.
* **Cart:** what you've picked. The **Download Text** and **Text Only (Skip Media)** boxes apply to the next send.
* **Console:** the log, including download progress.

***

## Columns

| Column | Meaning |
|---|---|
| **Number** | Row number |
| **Download Cart** | Cart control for sending downloads to the queue |
| **Username** | Creator's username |
| **Downloaded** | Boolean showing whether the database marks the media as downloaded |
| **Unlocked** | Boolean showing whether the post tied to the media is unlocked (a `null` value from the site shows as locked) |
| **Length** | Length of videos/audio formatted as `HH:MM:SS` (`N/A` for media without a length, such as pictures) |
| **`download_type`** | `normal`, `protected` (DRM), or `unknown` |
| **`other_posts_with_media`** | Identifies other posts with the same media ID |
| **Mediatype** | Type of media |
| **Post date** | Date the post was created or updated |
| **Post Media Count** | Number of media items in the post |
| **Responsetype** | Which API area the media came from |
| **Price** | Price of the post the media belongs to |
| **Post ID** | ID of the post the media belongs to |
| **Media ID** | ID of the media item |
| **Text** | Text from the post |

Post Media Count, Responsetype, Price, Post ID, and Media ID are hidden by default. Press `h` to show or hide them in the main and cart tables; the choice is remembered. Their filters still work while hidden.

***

## Picking media (the cart)

These keys work on the DataTable tab with both sidebars closed:

| Key | Adds to the cart |
|---|---|
| `a` / `Shift+A` | This page / everything the filters show |
| `u` / `Shift+U` | Same, but each media item once |
| `e` / `Shift+E` | Same, but only media that isn't downloaded yet |

| Key | Removes from the cart |
|---|---|
| `c` / `Shift+C` | This page / everything the filters show |
| `x` | Everything |

You can also click a row's **Download Cart** cell to add or remove it, or click the **Download Cart** header to add the page. Locked media can't be added. On the Cart tab, click `[added]` to remove a row, `c` removes the page, and `x` or `Shift+C` empties the cart.

***

## Downloading

Press **>> Send Downloads to OF-Scraper** (on the DataTable or Cart tab). The table switches to the Console, and each row's Download Cart cell shows `[downloading]`, then `[downloaded]`, `[skipped]`, or `[failed]`. A creator's cart downloads as one batch. You can keep picking and send more while it downloads.

* **Stop Downloads** (or **Ctrl+X**) empties the queue and stops the files in progress, while the table stays open. Files that didn't finish keep their part files and resume on the next run.
* A failed download refreshes only its own posts before it's retried, instead of the creator's whole area.
* Items skipped from the table aren't marked downloaded, and the Downloaded column updates straight away.

***

## Opening the download folder

* `o` (DataTable tab, sidebars closed) opens the highlighted row's folder. For a downloaded file, that's the folder holding it, with the file selected on Windows and macOS. Otherwise it's the creator's download folder.
* The **Open Download Folder** button opens the highlighted row's creator's download folder.
* On Linux without a desktop, the folder's path is shown instead.

**Ctrl+Q** closes the table.

***

## Sorting the table

Click any column header ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/14ca5b89-c9c1-44bc-936e-db4683f81823):

* First click sorts descending.
* Second click sorts ascending.
* Subsequent clicks alternate.

***

## Filtering of the table

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* Press `Ctrl+S` to toggle the filter sidebar.
* The filter form has fields for every column in the table.
* Click **Filter** to apply your filters.

### Adding value from table

1. Click a cell to highlight it.
2. Press `;` or `'` to copy that cell's value into the matching filter field.
3. Click **Filter** to apply.

#### Example

A cell containing `videos` is highlighted in the `mediatype` column:

<figure><img src="../../.gitbook/assets/img1.png" alt=""><figcaption></figcaption></figure>

Pressing `;` or `'` copies it into the filter form:

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Clicking **Filter** applies the change, showing only videos in the table:

![image](https://github.com/datawhores/OF-Scraper/assets/67020411/11911f08-2e0c-4759-b033-1fcaf40a5e6f)

### Pasting IDs

Paste numbers into the **Media ID** or **Post ID** filter. Pasting a temp file name such as `tempvid_<media id>_<post id>.part` fills both filters.

### Clearing filters

The **Clear Filters** button next to **Filter** clears every filter.

### Reset the table

Click the **Reset** button. Keep in mind that the program keeps the current table data in memory, so it won't fetch new data until you restart it.

### Example filter by all content with the text dog

![image](https://github.com/datawhores/OF-Scraper/assets/67020411/6f03fbe1-2ad9-4296-9b95-7a4cad874e36)

### Additional info about text filter

Searches use Python regex and always ignore case (including Exact Match), so `Dog` matches `dog`.

#### Searching for full string match

Matches text that is exactly `"dog"` rather than text that merely contains `"dog"`:

![image](https://github.com/datawhores/OF-Scraper/assets/67020411/010b2d9a-a841-4b96-85c2-220a1fbecafc)
