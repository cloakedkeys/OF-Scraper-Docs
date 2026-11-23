---
description: What this fork changes compared with upstream OF-Scraper
---

# Fork Changes

These docs cover **cloakedkeys/OF-Scraper-Community**. Its releases start at **3.15.0**, and this page lists what changed from 3.14.7 through **3.17.1**. Upstream [datawhores/OF-Scraper](https://github.com/datawhores/OF-Scraper) now takes these changes too.

> ℹ️ **`ofscraper` 3.14.7 and older on PyPI have none of the changes below.** Install `ofscraper-community`, or update `ofscraper`. See [Install](installation/).

## Downloads and file names

* **Different media no longer overwrite each other** when a file name template gives them the same name (for example a template built on `{text}` or `{model_username}`). The download is saved as `name_<media_id>` instead, and the database records the name each file was actually saved under. Controlled by [`filename_collision`](getting-started/config-options/file-output-options/#filename_collision). ([#116](https://github.com/cloakedkeys/OF-Scraper-Community/pull/116))
* **Recover files lost to earlier collisions** with an offline command that marks them for re-download. See [Recover Filename Collisions](using-the-scraper/recipes/recover-filename-collisions.md). ([#120](https://github.com/cloakedkeys/OF-Scraper-Community/pull/120))
* **`textlength` and `text_type_default` take effect.** The `text_type_default` setting is used unless `--text-type` is passed, `--textlength` works, and word mode counts whole words, including when `space_replacer` isn't a space. ([#95](https://github.com/cloakedkeys/OF-Scraper-Community/pull/95))
* **Finished downloads on mapped or network drives** are no longer reported as failed when the drive's path can't be resolved. ([#96](https://github.com/cloakedkeys/OF-Scraper-Community/pull/96))
* **Model names with emoji** no longer crash output on consoles that aren't UTF-8; unprintable characters show as `?`. ([#94](https://github.com/cloakedkeys/OF-Scraper-Community/pull/94))
* **Files whose names contain regex characters** (for example a banner uploaded as `Untitled design (7).png`) download instead of always failing with `missing ), unterminated subpattern`. ([#130](https://github.com/cloakedkeys/OF-Scraper-Community/pull/130))

## DRM (protected video)

* **Failed DRM downloads are no longer marked as successful.** Empty or playlist responses fail the download instead of producing a 0-byte file. ([#1](https://github.com/cloakedkeys/OF-Scraper-Community/pull/1))
* **Purchased timeline posts** request their keys from the post endpoint, fixing `403 Forbidden` key errors on paid timeline content. ([#98](https://github.com/cloakedkeys/OF-Scraper-Community/pull/98))
* **ffmpeg 6 or newer** is accepted, including 8.x and 9.x. ([#108](https://github.com/cloakedkeys/OF-Scraper-Community/pull/108))
* **Quoted paths** for the CDM files, `ffmpeg` and `temp_dir` are accepted, as produced by Windows' "Copy as path". An empty `ffmpeg` setting counts as unset. ([#97](https://github.com/cloakedkeys/OF-Scraper-Community/pull/97))
* **cdrm key mode** sends headers in the format the service expects and no longer shows a false startup warning. The public cdrm-project API appeared to be offline when this was tested. cdrm sends your request headers, cookies included, to a third-party site and is deprecated in the fork; use manual CDM. See [CDM Setup](cdm-options/). ([#99](https://github.com/cloakedkeys/OF-Scraper-Community/pull/99))

## Paid content (`--scrape-paid`)

* **Skip a model** with `--excluded-username`, which now applies to `--scrape-paid` for both downloads and metadata runs. See [`--excluded-username`](command-reference/shared-options/scrape-metadata-options/user-selection-options.md). ([#121](https://github.com/cloakedkeys/OF-Scraper-Community/pull/121))
* **`--scrape-paid` no longer crashes** with `UnboundLocalError` on every run. ([#122](https://github.com/cloakedkeys/OF-Scraper-Community/pull/122))
* **A Purchases scan that stops early** (HTTP error, unexpected response or exception) now logs a warning ending in "Purchases may be incomplete." ([#113](https://github.com/cloakedkeys/OF-Scraper-Community/pull/113))
* **Deleted accounts found by the paid scan** are no longer also put through the normal scrape, where each one failed with `KeyError: 'avatar'`. Their purchases are still downloaded by the paid pass. ([#129](https://github.com/cloakedkeys/OF-Scraper-Community/pull/129))
* **A deleted account's profile area** is skipped with a log line instead of failing with `KeyError: 'name'`. Its chat and messages are still scraped if OnlyFans still serves them. ([#128](https://github.com/cloakedkeys/OF-Scraper-Community/pull/128))

## Metadata

* **`metadata` with hashing enabled** no longer skips files with a `TypeError`. ([#123](https://github.com/cloakedkeys/OF-Scraper-Community/pull/123))
* **`metadata ... update`** keeps a media's recorded file when it still exists, so a renamed collision file isn't pointed at another media's file. ([#116](https://github.com/cloakedkeys/OF-Scraper-Community/pull/116))

## Daemon mode

* **`docker stop` and SIGTERM** stop a daemon-mode container promptly instead of waiting for Docker to kill it. ([#93](https://github.com/cloakedkeys/OF-Scraper-Community/pull/93))
* **SIGTERM or Ctrl+C while the daemon waits between passes** exits cleanly instead of failing with `ValueError: task_done() called too many times` and exit status 1. ([#126](https://github.com/cloakedkeys/OF-Scraper-Community/pull/126))
* **Trigger the next pass early** with SIGUSR1 (`docker kill --signal=SIGUSR1 <container>`) while the daemon is waiting. Docker/Linux only. See [`--daemon`](command-reference/shared-options/scrape-metadata-options/general-scraper-args.md). ([#125](https://github.com/cloakedkeys/OF-Scraper-Community/pull/125))

## Docker

* **Downloads go to the mounted data folder** (`/home/ofscraper/data`) by default, rather than `/home/ofscraper/Data/ofscraper`. ([#105](https://github.com/cloakedkeys/OF-Scraper-Community/pull/105))
* **`USER_ID`, `GROUP_ID`, `USER_NAME` and `GROUP_NAME`** from `docker-compose.yml` now take effect. ([#111](https://github.com/cloakedkeys/OF-Scraper-Community/pull/111))
* **Non-root containers** (`docker run --user` or compose `user:`) start instead of exiting. ([#104](https://github.com/cloakedkeys/OF-Scraper-Community/pull/104))
* **arm64 images** include a working ffmpeg (static 9.0.2; amd64 uses `pyffmpeg`'s ffmpeg). ([#103](https://github.com/cloakedkeys/OF-Scraper-Community/pull/103))

See [Docker](installation/docker.md) for details.

## Fansly (3.16.0)

* **Fansly as a second site.** Switch with `--site fansly` or a `site.json` in the profile folder. Fansly has its own login file. Posts, messages and purchases are downloaded, videos in the best quality as direct, HLS or DASH, and livestreams can be recorded with ffmpeg. See [Fansly](fansly.md). ([#158](https://github.com/cloakedkeys/OF-Scraper-Community/pull/158), [#159](https://github.com/cloakedkeys/OF-Scraper-Community/pull/159), [#160](https://github.com/cloakedkeys/OF-Scraper-Community/pull/160), [#161](https://github.com/cloakedkeys/OF-Scraper-Community/pull/161))

## Requests and downloads (3.16.0)

* **Stalled requests no longer hang a run.** Requests have a default read timeout, and stalled TLS handshakes time out. ([#167](https://github.com/cloakedkeys/OF-Scraper-Community/pull/167), [#152](https://github.com/cloakedkeys/OF-Scraper-Community/pull/152))
* **The download speed limit works** and is shared by all downloads. Retry and wait settings are used, and 0 is no longer replaced by the default. ([#172](https://github.com/cloakedkeys/OF-Scraper-Community/pull/172), [#169](https://github.com/cloakedkeys/OF-Scraper-Community/pull/169), [#177](https://github.com/cloakedkeys/OF-Scraper-Community/pull/177))
* **A cancelled request stops** instead of being retried, and failed downloads close their connection. ([#171](https://github.com/cloakedkeys/OF-Scraper-Community/pull/171), [#151](https://github.com/cloakedkeys/OF-Scraper-Community/pull/151))
* **Labels with nothing new** are no longer paged through again on every run. ([#150](https://github.com/cloakedkeys/OF-Scraper-Community/pull/150))

## Login and logs (3.16.0)

* **Clearer login problems.** A logged-out session is reported as bad auth, and network failures during the login check are reported as network errors. Typing "quit" or "main" at the auth prompt works. ([#178](https://github.com/cloakedkeys/OF-Scraper-Community/pull/178), [#170](https://github.com/cloakedkeys/OF-Scraper-Community/pull/170), [#175](https://github.com/cloakedkeys/OF-Scraper-Community/pull/175))
* **The OnlyFans session cookie is masked in every log line**, so logs are safer to share. ([#166](https://github.com/cloakedkeys/OF-Scraper-Community/pull/166))
* **Display fixes.** Log lines with broken formatting are kept, outside text is printed as plain text, and tables show other kinds of values. ([#189](https://github.com/cloakedkeys/OF-Scraper-Community/pull/189), [#191](https://github.com/cloakedkeys/OF-Scraper-Community/pull/191), [#193](https://github.com/cloakedkeys/OF-Scraper-Community/pull/193))

## Command line (3.16.0 and 3.16.1)

* **`--before` and `--after`** accept `MM/DD/YYYY` and relative dates such as "3 weeks ago". ([#148](https://github.com/cloakedkeys/OF-Scraper-Community/pull/148))
* **A mistake on the command line** prints a short usage message instead of a traceback, and **a failed run exits with status 1**. ([#196](https://github.com/cloakedkeys/OF-Scraper-Community/pull/196), [#149](https://github.com/cloakedkeys/OF-Scraper-Community/pull/149))
* **`--block-ads` is accepted**, **`--env-files` is loaded**, and **`--length-max`/`--length-min`** take whole seconds. ([#221](https://github.com/cloakedkeys/OF-Scraper-Community/pull/221))
* **Check commands:** the paid lookup no longer swaps the creator's name and id, `-f` username files work, and `msg_check` has its own help. ([#219](https://github.com/cloakedkeys/OF-Scraper-Community/pull/219), [#229](https://github.com/cloakedkeys/OF-Scraper-Community/pull/229))
* **`--dynamic-rules`** accepts the same rule names as the menu and `config.json`. ([#233](https://github.com/cloakedkeys/OF-Scraper-Community/pull/233))

## Settings and environment (3.16.0 and 3.16.1)

* **Settings in `config.json` are read as written.** This covers `incremental_downloads: false`, `cache-mode`, `responsetype.message`, a `download_sems` of 0 and upper-case names in user lists. A rejected `dynamic-mode-default` falls back to the default with a warning. ([#223](https://github.com/cloakedkeys/OF-Scraper-Community/pull/223))
* **A new `config.json`**, and any setting added to an older one, gets the built-in defaults instead of saving environment overrides as if you had chosen them. ([#228](https://github.com/cloakedkeys/OF-Scraper-Community/pull/228))
* **The dynamic rule menu** lists the default as `digital`, and the menu, `config.json` and the request code accept the same names. ([#230](https://github.com/cloakedkeys/OF-Scraper-Community/pull/230))
* **Environment variables:** settings given by key name alone are converted to the right type, `OFSC_BATCH_TEMPFILE_CLEANUP` accepts "true", batch cleanup also removes leftover `temp_` files, and `OFSC_DYNAMIC_RULE_MANUAL` is read as JSON. ([#183](https://github.com/cloakedkeys/OF-Scraper-Community/pull/183), [#185](https://github.com/cloakedkeys/OF-Scraper-Community/pull/185), [#187](https://github.com/cloakedkeys/OF-Scraper-Community/pull/187), [#163](https://github.com/cloakedkeys/OF-Scraper-Community/pull/163))

## Database, rate limits and likes (3.16.1)

* **Existing stories are updated**, messages keep their deleted flag, table rebuilds and merges keep every row, and CSV export writes every selected creator's rows. ([#222](https://github.com/cloakedkeys/OF-Scraper-Community/pull/222), [#231](https://github.com/cloakedkeys/OF-Scraper-Community/pull/231), [#211](https://github.com/cloakedkeys/OF-Scraper-Community/pull/211))
* **Backoff:** each backoff reads its own decay settings, the 403 backoff applies whatever the rate-limit gap is, and a rate-limit wait for downloads and likes ends once it decays below half a second. ([#208](https://github.com/cloakedkeys/OF-Scraper-Community/pull/208), [#217](https://github.com/cloakedkeys/OF-Scraper-Community/pull/217), [#227](https://github.com/cloakedkeys/OF-Scraper-Community/pull/227))
* **A like or unlike that fails** marks the post as failed, and `{my_id}` holds your account id, not your display name. ([#210](https://github.com/cloakedkeys/OF-Scraper-Community/pull/210), [#216](https://github.com/cloakedkeys/OF-Scraper-Community/pull/216), [#215](https://github.com/cloakedkeys/OF-Scraper-Community/pull/215))

## Scripts and docs (3.15.1 to 3.16.1)

* **Caption files** are written as UTF-8 with line breaks (3.15.1). ([#133](https://github.com/cloakedkeys/OF-Scraper-Community/pull/133))
* **`scripts/creator_names.py`** lists every name a creator account has gone by, finds accounts by an old name, and can record a name you learned elsewhere. ([#146](https://github.com/cloakedkeys/OF-Scraper-Community/pull/146))
* **`docker-compose.yml`** uses this fork's image. ([#142](https://github.com/cloakedkeys/OF-Scraper-Community/pull/142))
* **The fork's `reference/` folder** documents every command, option, setting, environment default, placeholder and database table. ([#199](https://github.com/cloakedkeys/OF-Scraper-Community/pull/199))

## Downloads, logs and output (3.16.2)

* **Resuming a download is reliable.** A half-finished file is only continued when it still matches the file on the server: same size and, where the server says, the same version. Otherwise it starts over. DRM video and audio tracks resume separately. ([#249](https://github.com/cloakedkeys/OF-Scraper-Community/pull/249), [#252](https://github.com/cloakedkeys/OF-Scraper-Community/pull/252), [#264](https://github.com/cloakedkeys/OF-Scraper-Community/pull/264))
* **Failed downloads stay failed.** An error page (404 and similar) or an empty reply is no longer saved as the media file and marked as downloaded. A download with no stated size is only accepted when a cut-off can be detected, and a retry keeps the half-finished file instead of starting from 0. ([#265](https://github.com/cloakedkeys/OF-Scraper-Community/pull/265), [#269](https://github.com/cloakedkeys/OF-Scraper-Community/pull/269), [#263](https://github.com/cloakedkeys/OF-Scraper-Community/pull/263), [#270](https://github.com/cloakedkeys/OF-Scraper-Community/pull/270))
* **Request headers are kept out of the purchased-content warning**, so login values don't end up in logs or Discord. ([#248](https://github.com/cloakedkeys/OF-Scraper-Community/pull/248))
* **`--output LOW` and `PROMPT`** now quiet the console as intended; prompts, errors and warnings you need to act on still show. `SUPRESS_*_DISPLAY=False` works, and these settings apply only while their screen is up. ([#257](https://github.com/cloakedkeys/OF-Scraper-Community/pull/257), [#258](https://github.com/cloakedkeys/OF-Scraper-Community/pull/258), [#266](https://github.com/cloakedkeys/OF-Scraper-Community/pull/266))
* **Importing ofscraper from another program** no longer reads that program's command line. ([#253](https://github.com/cloakedkeys/OF-Scraper-Community/pull/253))
* **On PyPI as `ofscraper-community`.** See [Install](installation/). ([#254](https://github.com/cloakedkeys/OF-Scraper-Community/pull/254))

## Resume and install (3.16.3 and 3.16.4)

* **An empty reply to a resumed download** keeps the half-finished file and its saved size, and a download cut off early usually keeps the bytes that arrived. ([#272](https://github.com/cloakedkeys/OF-Scraper-Community/pull/272))
* **Clearer install instructions and requirements:** Python 3.11 or higher, and ffmpeg 6 or newer for DRM video. ([#273](https://github.com/cloakedkeys/OF-Scraper-Community/pull/273), [#275](https://github.com/cloakedkeys/OF-Scraper-Community/pull/275))

## Fansly labels and quality (3.16.5)

* **`-o labels` works on Fansly.** Each profile tab is a label; add `{label}` to `dir_format` for a folder per tab. See [Fansly](fansly.md). ([#288](https://github.com/cloakedkeys/OF-Scraper-Community/pull/288))
* **Videos are no longer skipped or capped at 720p:** the largest version is downloaded, however Fansly offers it. ([#281](https://github.com/cloakedkeys/OF-Scraper-Community/pull/281))
* **Fansly `-u`** matches names in any case, and all-digit values match account ids. ([#283](https://github.com/cloakedkeys/OF-Scraper-Community/pull/283))
* **Runs without a terminal** log the problem and exit with status 1 instead of crashing on a question, and a daemon keeps going after an empty first scan. ([#289](https://github.com/cloakedkeys/OF-Scraper-Community/pull/289))
* **`--daemon -u` applies your filters**, including `--excluded-username`. ([#290](https://github.com/cloakedkeys/OF-Scraper-Community/pull/290))

## Skips, size limits, `ofscraper db` and Stash (3.16.6)

* **Size limits:** a file outside `-sm` / `-sx` is skipped, not failed, and tried again next run. A DRM video is checked as a whole. Rows the old behaviour saved as downloaded are repaired on first start. See [Media Filters Options](command-reference/shared-options/common-option-groups/media-filters-options.md#how-the-size-limits-work). ([#321](https://github.com/cloakedkeys/OF-Scraper-Community/pull/321), [#326](https://github.com/cloakedkeys/OF-Scraper-Community/pull/326), [#359](https://github.com/cloakedkeys/OF-Scraper-Community/pull/359))
* **`skip_download_script`:** `false` skips for this run only; `skip-permanent` skips for good, and `--retry-permanent-skips` or `ofscraper db --unmark-permanent-skips` undo it. See [Script Options](getting-started/config-options/script-options.md#skip-download-script-skip_download_script). ([#357](https://github.com/cloakedkeys/OF-Scraper-Community/pull/357), [#362](https://github.com/cloakedkeys/OF-Scraper-Community/pull/362))
* **`ofscraper db` only reads:** databases open read-only, older databases work, and `--post-id` / `--media-id` match. See [Database Command](page/database-command.md). ([#374](https://github.com/cloakedkeys/OF-Scraper-Community/pull/374), [#365](https://github.com/cloakedkeys/OF-Scraper-Community/pull/365), [#362](https://github.com/cloakedkeys/OF-Scraper-Community/pull/362))
* **Stash sync** copies your downloads' details into Stash. See [Organize Downloads in Stash](using-the-scraper/recipes/stash.md). ([#140](https://github.com/cloakedkeys/OF-Scraper-Community/pull/140))
* **Merging databases** keeps the downloaded state and post links, and a failed database no longer crashes the merge. ([#297](https://github.com/cloakedkeys/OF-Scraper-Community/pull/297), [#301](https://github.com/cloakedkeys/OF-Scraper-Community/pull/301))
* **Posts with no date** are kept and downloaded with their media's date, and the last page of a timeline, archived or streams scan is kept. ([#370](https://github.com/cloakedkeys/OF-Scraper-Community/pull/370), [#330](https://github.com/cloakedkeys/OF-Scraper-Community/pull/330))
* **A failed creator is named** in a warning and the run moves on. ([#380](https://github.com/cloakedkeys/OF-Scraper-Community/pull/380))

## Security and scripts (3.16.7)

* **The API cache is read as plain data only** (CVE-2025-69872), and packages with known vulnerabilities are updated. ([#399](https://github.com/cloakedkeys/OF-Scraper-Community/pull/399), [#400](https://github.com/cloakedkeys/OF-Scraper-Community/pull/400))
* **Scripts:** they get their whole input, their answer is used as soon as they exit, and stopping OF-Scraper stops them and the programs they started. See [How scripts run](getting-started/config-options/script-options.md#how-scripts-run). ([#385](https://github.com/cloakedkeys/OF-Scraper-Community/pull/385), [#393](https://github.com/cloakedkeys/OF-Scraper-Community/pull/393), [#388](https://github.com/cloakedkeys/OF-Scraper-Community/pull/388))
* **More auth values are masked** in logs. ([#397](https://github.com/cloakedkeys/OF-Scraper-Community/pull/397))

## Stopping, Esc and the check table (3.16.8 and 3.16.9)

* **Stop without quitting:** the first Ctrl+C stops downloads or the fetch, a second quits, and Esc goes back from any prompt. See [Using Prompts](using-the-scraper/using-prompts/#going-back-and-stopping). ([#451](https://github.com/cloakedkeys/OF-Scraper-Community/pull/451), [#453](https://github.com/cloakedkeys/OF-Scraper-Community/pull/453), [#449](https://github.com/cloakedkeys/OF-Scraper-Community/pull/449))
* **Fansly recordings stop cleanly**, keeping what was recorded. ([#452](https://github.com/cloakedkeys/OF-Scraper-Community/pull/452))
* **Check table:** open it from the Action Menu, Stop Downloads (Ctrl+X), open the download folder (`o`), hide columns (`h`), paste IDs, Clear Filters, and a failed download refreshes only its own posts. See [Table Management](content-check-modes/table-management/). ([#436](https://github.com/cloakedkeys/OF-Scraper-Community/pull/436), [#434](https://github.com/cloakedkeys/OF-Scraper-Community/pull/434), [#470](https://github.com/cloakedkeys/OF-Scraper-Community/pull/470), [#460](https://github.com/cloakedkeys/OF-Scraper-Community/pull/460), [#463](https://github.com/cloakedkeys/OF-Scraper-Community/pull/463))
* **An expired signed link fails at once** instead of being retried for a minute. ([#462](https://github.com/cloakedkeys/OF-Scraper-Community/pull/462))
* **Prompts redraw cleanly** after a terminal resize. ([#469](https://github.com/cloakedkeys/OF-Scraper-Community/pull/469), [#477](https://github.com/cloakedkeys/OF-Scraper-Community/pull/477))
* **Dependencies upgraded** and audited with `pip-audit`. ([#405](https://github.com/cloakedkeys/OF-Scraper-Community/pull/405), [#407](https://github.com/cloakedkeys/OF-Scraper-Community/pull/407))

## Fansly streams and UTF-8 scripts (3.16.10)

* **Fansly stream segments download in parallel and resume.** See [Streamed videos](fansly.md#streamed-videos). ([#295](https://github.com/cloakedkeys/OF-Scraper-Community/pull/295), [#483](https://github.com/cloakedkeys/OF-Scraper-Community/pull/483), [#484](https://github.com/cloakedkeys/OF-Scraper-Community/pull/484))
* **Scripts get UTF-8 text on Windows.** ([#481](https://github.com/cloakedkeys/OF-Scraper-Community/pull/481))

## Downloads after an IP change (3.16.11 to 3.16.13)

* **A link rejected with a 403** after a reconnect or VPN switch is fetched again and the download resumes. This covers posts, messages, purchases, stories, highlights and DRM video. ([#489](https://github.com/cloakedkeys/OF-Scraper-Community/pull/489), [#490](https://github.com/cloakedkeys/OF-Scraper-Community/pull/490))
* **Dependency updates** in 3.16.13. ([#491](https://github.com/cloakedkeys/OF-Scraper-Community/pull/491))

## Check table and creator picker (3.17.0)

* **Size limits** are entered as a number and a unit (Bytes, KB, MB, GB), and the table says when they apply. ([#514](https://github.com/cloakedkeys/OF-Scraper-Community/pull/514), [#522](https://github.com/cloakedkeys/OF-Scraper-Community/pull/522), [#527](https://github.com/cloakedkeys/OF-Scraper-Community/pull/527))
* **Right-click** copies a username or post id; right-click the Media ID or Post ID box to paste. ([#529](https://github.com/cloakedkeys/OF-Scraper-Community/pull/529))
* **The username filter** matches part of a name, and Clear Filters empties it. ([#526](https://github.com/cloakedkeys/OF-Scraper-Community/pull/526), [#525](https://github.com/cloakedkeys/OF-Scraper-Community/pull/525))
* **The length boxes** show which is hours, minutes and seconds. ([#518](https://github.com/cloakedkeys/OF-Scraper-Community/pull/518), [#528](https://github.com/cloakedkeys/OF-Scraper-Community/pull/528))
* **Enter on the Number cell** adds or removes the row, like the Download cell. ([#515](https://github.com/cloakedkeys/OF-Scraper-Community/pull/515))
* **A table with several creators** no longer crashes, and a creator OnlyFans can't find is skipped instead of stopping the check. ([#519](https://github.com/cloakedkeys/OF-Scraper-Community/pull/519), [#520](https://github.com/cloakedkeys/OF-Scraper-Community/pull/520))
* **Creator picker:** search matches the typed text in usernames only, Ctrl+A selects everything shown, Ctrl+D clears the selection, and Down on an empty search no longer crashes. ([#531](https://github.com/cloakedkeys/OF-Scraper-Community/pull/531), [#530](https://github.com/cloakedkeys/OF-Scraper-Community/pull/530), [#513](https://github.com/cloakedkeys/OF-Scraper-Community/pull/513))
* **"Yes Update Selection"** opens the picker with nothing ticked, and Esc keeps the creators you ticked. ([#511](https://github.com/cloakedkeys/OF-Scraper-Community/pull/511), [#524](https://github.com/cloakedkeys/OF-Scraper-Community/pull/524))
* **Help notes that Ctrl+V pastes** in Windows Terminal; use Alt+V there. ([#512](https://github.com/cloakedkeys/OF-Scraper-Community/pull/512))

## Settings, scans and labels (3.17.0)

* **The config menu** takes sizes and the download speed as a number and a unit. ([#516](https://github.com/cloakedkeys/OF-Scraper-Community/pull/516))
* **Unusual `config.json` contents** no longer crash or lose saved values. ([#503](https://github.com/cloakedkeys/OF-Scraper-Community/pull/503), [#508](https://github.com/cloakedkeys/OF-Scraper-Community/pull/508))
* **A scan that lost a page** is rescanned next run instead of skipping posts. ([#501](https://github.com/cloakedkeys/OF-Scraper-Community/pull/501))
* **Label names are decoded** (`&amp;` becomes `&`), and `{label}` folders use the decoded name. ([#523](https://github.com/cloakedkeys/OF-Scraper-Community/pull/523))
* **Only busy-database errors are retried.** ([#506](https://github.com/cloakedkeys/OF-Scraper-Community/pull/506))
* **The full-rescan hint** says what the redownload answer adds. ([#517](https://github.com/cloakedkeys/OF-Scraper-Community/pull/517))
* **Docker images** are also tagged with the release number. ([#495](https://github.com/cloakedkeys/OF-Scraper-Community/pull/495))

## Fansly links, rate limits and Python (3.17.1)

* **A Fansly link the CDN rejects** (403) is fetched again, up to 3 times, instead of failing the item. ([#537](https://github.com/cloakedkeys/OF-Scraper-Community/pull/537))
* **The rate-limit backoff starts** when a minimum gap between requests is set, instead of staying at the gap after a 429. ([#535](https://github.com/cloakedkeys/OF-Scraper-Community/pull/535))
* **Installing on a newer Python** gets the current release instead of an old one: there is no upper Python version limit any more. ([#533](https://github.com/cloakedkeys/OF-Scraper-Community/pull/533))

## Python

* **Python 3.11 or newer** is supported (CI tests on 3.11 and 3.15.2). Docker images and release binaries use 3.15.1. ([#109](https://github.com/cloakedkeys/OF-Scraper-Community/pull/109))

## Version check

* **The start-up update check** only reports a new version when PyPI's release is higher than the running one, so fork builds ahead of upstream's PyPI release (3.15.0 and later) aren't told to "update" to 3.14.7. ([#132](https://github.com/cloakedkeys/OF-Scraper-Community/pull/132))
* **The update check looks up `ofscraper-community` on PyPI**, so it reports the fork's releases instead of upstream's. If the check can't reach PyPI, the run carries on. ([#254](https://github.com/cloakedkeys/OF-Scraper-Community/pull/254))
