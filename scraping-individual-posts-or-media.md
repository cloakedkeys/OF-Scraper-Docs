# Scraping Individual Posts or Media

***

## Scraping content from timeline post

1. Click `...` and select **Copy link to post**:

   ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/84a87986-36ef-4d75-a9d9-10d7b572419a)

2. Run manual mode with the copied link:

   ```sh
   ofscraper manual --url copied_link
   ```

   Or pass the post ID directly:

   ```sh
   ofscraper manual --url postid
   ```

Manual mode downloads again even if the file is already in the database.

***

## Scraping content from purchase page

1. Click `...` and select **Copy link to message**:

   ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/74cebb3f-c0e4-4cbb-b2f7-18b52e2a98a6)

2. Run manual mode with the copied link:

   ```sh
   ofscraper manual --url copied_link
   ```

***

## Advanced

Check `get_info` in `manual.py` to see the full range of URL formats accepted by manual mode.

***

## Scraping Individual Media

1. **Run a content check mode:** See [Content Check Modes](content-check-modes/).
2. **Select rows to download:** Click a row's **Download Cart** cell, or use the cart keys `a`, `e`, or `u`. (`;` and `'` copy the highlighted cell's value into that column's filter.)
   * Only unlocked media can be added; rows showing `Not Unlocked` or `Unknown` can't be added.
   * Media marked for download shows `[added]`.

   ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/48e3badd-5502-480b-aeaa-04d58c769dd1)

3. **Click `>> Send Downloads to OF-Scraper`:**

   ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/9727c122-73ea-4043-850a-4d4fe0ffbf33)

   Download progress updates in the console:

   ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/9d0748b2-c036-4b7f-91c0-499b78a808e1)

4. **Finished downloads show `[downloaded]`:**

   ![image](https://github.com/datawhores/OF-Scraper/assets/67020411/7ae553c7-94d1-4a03-a44f-83fd056b80f9)

To download an item again, click a `[downloaded]`, `[failed]`, `[stopped]`, or `[skipped]` cell once; it goes back to `[added]`.

| Status | Meaning |
|---|---|
| `[added]` | Content is ready to be added to the queue |
| `[downloading]` | Content is added to the queue and will be downloaded |
| `[downloaded]` | Content was downloaded and post-processing succeeded |
| `[failed]` | Content wasn't downloaded or post-processing failed |
| `[stopped]` | Stopped with `Ctrl+X` |
| `[skipped]` | Skipped by the size limits or a skip script, and not recorded as downloaded |

Rows still waiting when you press **Stop** go back to `[added]`. Rows showing `Not Unlocked` or `Unknown` can't be added.

### Good things to know

* Downloads start within about a second of pressing `>> Send Downloads to OF-Scraper`.
* Since there isn't a progress bar, enabling debug mode can help track progress.
* You can click the table to add more downloads at any time; entries marked `[downloading]` can't be modified.
* Sorting and filtering remain available while downloading.
