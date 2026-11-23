---
description: Automate liking & downloading OnlyFans posts
---

# Basic Automation with command-line

***

## Basic Run

Running with no arguments opens the interactive prompt menus:

```sh
ofscraper
```

* [Downloading Content](basic-actions/selecting-posts/)
* [Model Filtering/Sorting](model-selection-sorting/)
* [Liking/Unliking Post](basic-actions/liking-unliking-post.md)

***

## Performing action(s)

> ℹ️ `--posts` is shorthand used for all actions unless `--like-area` or `--download-area` is passed.

You can combine these actions:

* `like` or `unlike` (only one, because liking and unliking all posts at once doesn't make sense)
* Either of those combined with `download`

Download all wall posts for the selected creator and like them at the same time:

```sh
ofscraper --posts all --action like,download
```

Download only:

```sh
ofscraper --posts all --action download
```

### Selecting different areas

You can set separate areas for each action:

* `--like-area` for `like`/`unlike`
* `--download-area` for `download`

Download all posts, but only like pinned posts:

```sh
ofscraper --download-area all --like-area pinned --action like,download
```

Or:

```sh
ofscraper --posts all --like-area pinned --action like,download
```

***

## Bypass all prompts

> ℹ️ To bypass the like-area prompt when running `like` or `unlike`, pass `--like-area` or include `timeline`, `pinned`, `archived`, `streams`, `labels`, `all`, `labels+`, or `labels*` in `--posts`.

To bypass all prompts:

* Select at least one scraping action (`--action`)
* Provide one or more usernames (`--username`)
* Provide the areas to scan (`--posts`, `--download-area`, or `--like-area`)

```sh
ofscraper --posts all --username ALL --action like,download
```

***

## Running command in the background

For daemon mode to run, you must select at least one scraping action.

> ℹ️ In daemon mode, if `--username` isn't provided, OF-Scraper prompts you to pick creators only once.

> ℹ️ In daemon mode, if `--posts` or `--scrape-paid` isn't provided, OF-Scraper prompts you to pick areas only once.

```sh
ofscraper --daemon 10 --posts all --action like,download
```

This runs at least every 10 minutes. If a run takes longer than 10 minutes, the next run starts immediately after the previous one finishes. `--daemon` (`-d`) takes the interval in minutes, and decimals are allowed.

### Trigger the next pass early

> ℹ️ **Since 3.15.0, Docker/Linux.** See [Fork Changes](../../fork-changes.md).

While the daemon is waiting between runs, send `SIGUSR1` to start the next run without restarting it:

```sh
docker kill --signal=SIGUSR1 <container>
```

Outside Docker, `kill -USR1 <pid>` does the same.

* The signal is ignored during an active run. Repeated signals don't queue extra runs.
* After the triggered run, the normal interval starts again.
* SIGTERM and Ctrl+C still shut the daemon down, including while it's waiting between runs.
* Native Windows has no SIGUSR1, so this isn't available there.

***

## Modifications to Filename

### Toggle letter count for textlength

`textlength` counts either words or letters. Choose with `--text-type` (`word` or `letter`) or `text_type_default` in `config.json`:

```sh
ofscraper --text-type letter
```

* `word` splits the text placeholder into words (on `space_replacer`, or a space) and counts words.
* `letter` counts characters.

### Other filename options

These override the matching [File Output Options](../../getting-started/config-options/file-output-options/README.md) for one run:

| Option | What it does | Example |
|---|---|---|
| `--textlength` (`-tl`) | Maximum length of the text placeholder, in the `--text-type` unit. Keeps long post text within OS limits. | `-tt letter -tl 10` keeps at most 10 characters |
| `--space-replacer` (`-sr`) | Replaces spaces in the filename text with the given character, for file systems or apps that don't handle spaces well. | `-sr _` turns `This File.txt` into `This_File.txt` |
| `--original` (`-g`) | Turns off truncation of long file paths, so names aren't shortened. | `-g` |

When truncation happens, it uses the `--text-type` unit, the `--textlength` length and the current OS limits.

***

### Output Options

[Controlling Output/Logs](../../getting-started/controlling-output.md)
