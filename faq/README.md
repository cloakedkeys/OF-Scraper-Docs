# FAQ/Common Issues

## 1. Missing Post

Some creators delete content, which prevents OF-Scraper from accessing it.

***

## 2. Number of users doesn't match account number

See [upstream issue #224](https://github.com/datawhores/OF-Scraper/issues/224#issuecomment-1757367312).

Each page request asks the API for 10 names, but fewer than 10 are often returned.

### Example

Account: 400 total subscriptions.

* **Active accounts:** More accurate, though it updates on a schedule and can be slightly off until synchronisation runs.
* **Expired and `ALL`:** Significantly affected by expired subscriptions. As OnlyFans steps through offsets `[0, 10, 20, 30, ..., 390]`, some offsets return fewer than 10 entries, reducing the final count.

***

## 3. Missing Models

Before opening an issue, make sure you're on the latest version.

***

## 4. Lots of tempvideo or tempaudio files

Make sure your CDM (Content Decryption Module) is set up correctly and `ffmpeg` 6 or newer is installed. Manual CDM is recommended.

See [CDM Options](../cdm-options/README.md).

***

## 5. Something is not working

Display debug output in the console:

```sh
ofscraper --output debug
```

Or write debug logs to your configuration folder:

```sh
ofscraper --log debug
```

Attach the log to a GitHub issue (or share it in Discord).

***

## 6. FFMPEG

`ffmpeg` 6 or newer is required for downloading protected content. See [FFmpeg Downloads](https://ffmpeg.org/download.html).

#### Binaries

> ℹ️ If you download `ffmpeg` manually, put its full path in `config.json`.

See [Binaries Options](../getting-started/config-options/binaries-options.md).

<details>

<summary>Copying a path on Windows</summary>

If Windows doesn't give you an easy way to copy a file path, you can use [Path Copy Copy](https://pathcopycopy.github.io/).

</details>

***

## 7. ofscraper not found

This usually means you need to add the install folder to your `PATH`.

***

## 8. Can this download locked content

Yes, if it was unlocked before.

***

## 9. Status Down

This usually means your authentication details are wrong, or you've been signed out of OnlyFans.

***

## 10. 404 Response

The content is no longer available, or the creator has deleted their account.

***

## 11. Request taking a long time

When a request fails, OF-Scraper pauses and retries several times. Frequent retries can make runs take longer.

> ℹ️ Requests have a built-in time limit so they don't hang forever (the read timeout is 60 seconds by default). You can override that default by setting the `OFSC_READ_TIMEOUT` environment variable.

***

## 12. 429 Response

* Usually caused by too many requests, especially when auto-liking or unliking.
* The limit appears to be around 1,000 per day.

***

## 13. 409 Response

Content is unavailable on the OnlyFans site itself (shown as placeholders or media that won't load).

VPN users often see this depending on which VPN server they're connected to; it also affects the API, so OF-Scraper can't scrape that content either. Switch VPN servers, or wait a while for it to reset.

***

## 14. Scrape entire paid page or --scrape-paid should I do it

This depends on how much content you've purchased.

#### Does the regular scraper get purchased content?

Yes. When you include `purchased`, OF-Scraper scans purchased content for the selected creators by looking up their usernames on the purchases page.

#### Then why the prompt

Creators with deleted accounts have no username to look up, so scanning the entire purchases page is the only way to find their purchases.

#### When would you use it

Use it for your initial scan, or if you run scans infrequently.

#### When would you not use it

If you run frequent scans (such as daily), you can leave it off for most runs.

***

## 15. FFmpeg shared library not found Error

Example: ``version `GLIBCXX_3.4.29' not found``

### Cause

Missing shared libraries (Linux only).

### Fix

Use the GPL non-shared release build from [BtbN FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds/releases).

### Some Info

* [Which version of ffmpeg is the latest? (Super User)](https://superuser.com/questions/1712179/which-version-of-ffmpeg-is-the-latest)
* The version in your Linux distribution's repository may not work.

***

## 16. CDM Issues

See [CDM issues](../cdm-options/cdm-issues.md).

***

## 17. Trouble logging in

* Check the formatting of `auth.json` (see [Auth](../getting-started/auth.md)).
* Use `--auth-fail` to make a run quit on an auth error instead of prompting again.
* Try changing `dynamic-mode-default` (see [Advanced config options](../getting-started/config-options/options/advanced-config-options.md)).

***

## 18. Support For Network Drives

Network drives have limited support for storing media, and aren't supported at all for config files or databases. Store config files and databases on a local drive.

***

## 19. "Double check auth info"

* Copy every value (`sess`, `auth_id`, `x-bc`, `user_agent`) again from the same browser while you're logged in to OnlyFans. They expire when you log out.
* `user_agent` must match that browser exactly.
* Make sure you're on the latest version of this fork.

***

## 20. "No accounts found during scan"

Usually an auth problem, so check the answer above first. Then check you have an active subscription to the creator, and that you aren't filtering it out with options like `--expired-subscription`.

***

## 21. Files download fine but are counted as "failed"

Fixed in 3.15.0. This mostly happened when saving to a mapped or network drive. Update to the latest version.

***

## 22. Some messages or new posts are missing

A bug that skipped messages when using `--after` is fixed in 3.15.0. Update, then run again. To rescan a date range, add `--after YYYY-MM-DD`. Add `--force-all` as well if you want files you already have downloaded again.

***

## 23. ffmpeg isn't found even though it's installed

Put the full path to the `ffmpeg` program in `binary_options` → `ffmpeg` in your config, for example `C:\ffmpeg\bin\ffmpeg.exe`. An empty setting means "not set".

***

## 24. It says to update to 3.14.7

3.14.7 is the last of upstream's old `ofscraper` releases on PyPI, and it's older than this fork's code. Version 3.15.0 and later no longer show that message. From 3.16.2 the update check looks up `ofscraper-community`; from 3.17.0 it looks up the package you installed (`ofscraper-community`, or `ofscraper`, which `datawhores/OF-Scraper` now publishes from the same code).

***

## 25. Two files saved with the same name overwrote each other

Newer versions save the second one as `name_<media_id>` instead. To recover files lost to this in older versions, see [Recover Filename Collisions](../using-the-scraper/recipes/recover-filename-collisions.md).

***

## 26. Fansly login or download problems

See [Fansly](../fansly.md) for how to get the token and user agent.

***

## 27. Downloads fail with 403 after a reconnect or VPN switch

OnlyFans download links are signed for the IP that fetched them. From 3.16.11, a link rejected with a 403 is fetched again and the download resumes from its `.part` file; 3.16.12 extends this to stories, highlights, and DRM video. Update if every remaining download fails after your IP changes.

***

## 28. Files skipped by the size limits or skip script come back

That's intended from 3.16.6: a skip is for this run only, so the file is tried again next run. To skip a file for good, have the skip download script print `skip-permanent`. See [Script Options](../getting-started/config-options/script-options.md).
