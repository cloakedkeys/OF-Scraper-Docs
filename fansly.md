---
description: Using Fansly instead of OnlyFans
---

# Fansly

Since 3.16.0 OF-Scraper can download from Fansly as well as OnlyFans. A run uses one site at a time, and each site has its own login.

> ℹ️ **Not in 3.14.7**, the last of the old `ofscraper` releases. Use `ofscraper-community` 3.16.0 or later, or `ofscraper` 3.17.0 or later (`datawhores` now publishes it from the same code). See [Fork Changes](fork-changes.md).

***

## What is supported

* **Posts, messages and purchases** (`-o timeline,messages,purchased`).
* **Labels** (`-o labels`, `labels+`, `labels*`): each tab on a creator's profile is a label. The main "Posts" tab is the whole timeline, so it's skipped. Labels are recorded in the database; add `{label}` to `dir_format` for a folder per tab.
* Other areas (pinned, archived, stories, highlights, streams, profile) are skipped with a log line.
* **Videos** download in the largest version available, whether Fansly serves them as a direct file, an alternate copy, HLS or DASH. Streamed videos need ffmpeg.
* **Livestream recording** with ffmpeg (see below).

`-u` names match in any case, and an all-digit `-u` or `-eu` value also matches an account id. This applies to `--live` too.

***

## Streamed videos

HLS stream videos are fetched several segments at a time, then joined by ffmpeg without re-encoding.

* `FANSLY_STREAM_SEGMENTS` (environment variable `OFSC_FANSLY_STREAM_SEGMENTS`, default 8) sets how many segments download at once. `0` leaves the whole stream to ffmpeg, with no resume.
* **A stopped stream download resumes.** Fetched segments are kept in a hidden `.<part name>.segments` folder beside the part file, and the next run fetches only the missing ones. If the stream or quality changed, it starts over. With `--no-auto-resume` or `auto_resume: false`, nothing is kept.
* Plain HLS, AES-128 encrypted HLS, HLS byte ranges and unprotected static DASH use this downloader. Live HLS, other encryption methods, and protected, live or multi-period DASH go to ffmpeg alone and don't resume.

Fansly media are saved under `<save_location>/Fansly`, and each creator's `user_data.db` for Fansly is kept apart from the OnlyFans one.

***

## Switching to Fansly

A profile belongs to one site. The site is chosen in this order:

1. `--site` for one run
2. `site.json` in the profile folder
3. OnlyFans, if neither is set

### For one run

```sh
ofscraper --site fansly
```

### For a profile

Create `site.json` in the profile folder (`~/.config/ofscraper/main_profile/` by default) with:

```json
{
    "site": "fansly"
}
```

To keep both sites, use a separate profile for Fansly with the `--profile` option.

> ℹ️ **`--site` accepts `onlyfans` or `fansly`.**

***

## Fansly auth

Fansly credentials are kept in `fansly_auth.json` in the profile folder, not in `auth.json`. If the file is missing or incomplete, OF-Scraper asks for the values when you run it on Fansly.

```json
{
    "authorization_token": "",
    "user_agent": "",
    "check_key": ""
}
```

| Field | What it is |
| --- | --- |
| `authorization_token` | The token Fansly gives your logged in browser. Required. |
| `user_agent` | The User-Agent of the browser the token came from. Required. |
| `check_key` | Optional. The web app's current check key. A built-in value is used when this is empty. Fansly changes it from time to time, so set it if requests start failing. |

`device_id` and `device_id_fetched_at` are filled in by the program. You don't need to set them.

### Getting the token

1. Log in to fansly.com in your browser and open the developer tools (see [Auth](getting-started/auth.md) for the keys).
2. Go to `Application`, then `Local Storage`, then `session_active_session`, and copy the value of `token`.\
   Or copy the `authorization` header of any request to the Fansly API.
3. Copy your browser's `User-Agent` from a request header.
4. Paste both into the prompt, or into `fansly_auth.json`.

> ℹ️ **The token is entered without a "Bearer" prefix.** OF-Scraper removes the prefix if you paste it. The token is masked in logs.

***

## Livestreams

These options only apply to Fansly profiles and do nothing on OnlyFans. They're accepted by the main program (no subcommand).

| Option | What it does |
| --- | --- |
| `--live` | Record the selected creators who are live now (all followed creators without `-u`), then continue |
| `--live-watch` | Keep checking who is live and record them. With `--daemon` it runs beside the scheduled scrapes |
| `--live-interval` | Seconds between live checks in `--live-watch` (whole number, at least 10; default 60, plus up to 10 seconds of jitter) |
| `--live-max` | Most livestreams recorded at the same time (whole number, at least 1; default 2) |
| `--live-chat` | Also save the livestream chat to a `.jsonl` file. Off by default |

Recordings are saved as MP4 with a `.json` file beside them. If a recording drops, it continues in a new part. Stopping a recording (Ctrl+C with `--live`, or daemon shutdown) tells ffmpeg to finish and close the file, so what was recorded is kept. ffmpeg is killed only if it hasn't exited after 15 seconds.

***

## Example

```sh
ofscraper --site fansly --action download --usernames creatorname
```

See [Command Reference](command-reference/README.md) for the other options.
