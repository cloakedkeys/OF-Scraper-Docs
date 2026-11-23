---
description: Configure automated actions, daemon mode and Fansly livestream recording.
---

# Automation Options

## Background Execution

### -d, --daemon \[argument]

* **Runs:** Runs the program in the background as a daemon.
* **Argument (required):** Interval in minutes between runs; decimals are allowed (e.g. `-d 60` for hourly runs).

#### Trigger the next pass early

> ℹ️ **Since 3.15.0, Docker/Linux.** See [Fork Changes](../../../fork-changes.md).

While the daemon is waiting between passes, send `SIGUSR1` to start the next pass without restarting it:

```sh
docker kill --signal=SIGUSR1 <container>
```

Outside Docker, `kill -USR1 <pid>` does the same.

* The signal is ignored during an active pass. Repeated signals don't queue extra passes.
* After the triggered pass, the normal interval starts again.
* SIGTERM and Ctrl+C still shut the daemon down, including while it's waiting between passes.
* Native Windows has no SIGUSR1, so this isn't available there.

## Automated Actions

### -a, --action (also `--actions`) \[argument]

* **Selects:** The automated action to run on posts.
* **Possible choices:**
  * `like`: Likes each processed post.
  * `unlike`: Unlikes each processed post.
  * `download`: Downloads media (images, videos, audio) from each processed post.
* **Combined actions:** Repeat `-a` or separate choices with a comma (for example, `-a like -a download` or `-a like,download`). `like` and `unlike` can't be combined.

> ℹ️ **Like and unlike are subject to rate limits.**

## Fansly Livestreams

These options apply to Fansly only (`--site fansly`) and are available in the main program.

### --live

* Records the selected creators (all followed creators without `-u`) who are live now, then continues.

### --live-watch

* Keeps checking who is live and records them. With `--daemon` it runs beside the scheduled scrapes.

### --live-interval \[argument]

* Seconds between live checks in `--live-watch`. Whole number, at least 10 (default 60, plus up to 10 seconds of jitter).

### --live-max \[argument]

* The most livestreams recorded at the same time. Whole number, at least 1 (default 2).

### --live-chat

* Also saves livestream chat to a `.jsonl` file (read-only; off by default).
