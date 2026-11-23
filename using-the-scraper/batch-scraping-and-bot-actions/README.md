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

This runs at least every 10 minutes. If a run takes longer than 10 minutes, the next run starts immediately after the previous one finishes.

On Linux and in Docker, send `SIGUSR1` while the daemon is waiting between runs to start the next run early. It is ignored while a run is active:

```sh
docker kill --signal=SIGUSR1 <container>
```

***

## Modifications to Filename

### Toggle letter count for textlength

`textlength` counts either words or letters. Choose with `--text-type` (`word` or `letter`) or `text_type_default` in `config.json`:

```sh
ofscraper --text-type letter
```

***

### Output Options

[Controlling Output/Logs](../../getting-started/controlling-output.md)
