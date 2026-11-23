# Missing Posts & Models

## Missing Post

Some creators delete content, which prevents OF-Scraper from accessing it.

***

## Some messages or new posts are missing

A bug that skipped messages when using `--after` is fixed in 3.15.0. Update, then run again. To rescan a date range, add `--after YYYY-MM-DD`. Add `--force-all` as well if you want files you already have downloaded again.

***

## Number of users doesn't match account number

See [upstream issue #224](https://github.com/datawhores/OF-Scraper/issues/224#issuecomment-1757367312).

Each page request asks the API for 10 names, but fewer than 10 are often returned.

### Example

Account: 400 total subscriptions.

* **Active accounts:** More accurate, though it updates on a schedule and can be slightly off until synchronisation runs.
* **Expired and `ALL`:** Significantly affected by expired subscriptions. As OnlyFans steps through offsets `[0, 10, 20, 30, ..., 390]`, some offsets return fewer than 10 entries, reducing the final count.

***

## Missing Models

Before opening an issue, make sure you're on the latest version.

***

## Can this download locked content

Yes, if it was unlocked before.

***

## Scrape entire paid page or `--scrape-paid`: should I do it

This depends on how much content you've purchased.

#### Does the regular scraper get purchased content?

Yes. When you include `purchased`, OF-Scraper scans purchased content for the selected creators by looking up their usernames on the purchases page.

#### Then why the prompt

Creators with deleted accounts have no username to look up, so scanning the entire purchases page is the only way to find their purchases.

#### When would you use it

Use it for your initial scan, or if you run scans infrequently.

#### When would you not use it

If you run frequent scans (such as daily), you can leave it off for most runs.
