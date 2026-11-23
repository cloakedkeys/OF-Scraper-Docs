---
description: The most common commands, and where every option is described.
---

# Command Reference

Every command and option, with its short form, default and the `config.json` setting it replaces, is in [Command-line options](../reference/cli.md) in the Technical Reference. That page is built from the code, so it matches the release it describes.

## Syntax

```
ofscraper [options]
ofscraper [subcommand] [subcommand options]
```

> ℹ️ **Fork:** a failed run exits with status 1, and bad command-line input prints a short usage message. See [Fork Changes](../fork-changes.md).

## Common commands

| Task | Command | Guide |
|---|---|---|
| Open the menus | `ofscraper` | [Using Prompts](../using-the-scraper/using-prompts/README.md) |
| Download everything from every creator, no prompts | `ofscraper --posts all --username ALL --action download` | [Basic Automation with command-line](../using-the-scraper/batch-scraping-and-bot-actions/README.md) |
| Like posts | `ofscraper --posts timeline --action like` | [Liking/Unliking Post](../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/liking-unliking-post.md) |
| Run on a schedule | `ofscraper --daemon 60 --posts all --action download` | [Running command in the background](../using-the-scraper/batch-scraping-and-bot-actions/README.md#running-command-in-the-background) |
| Download one post | `ofscraper manual --url <link>` | [Scraping Individual Posts or Media](../using-the-scraper/scraping-individual-posts-or-media.md) |
| Browse and pick media | `ofscraper post_check --url <link or username>` | [Content Check Modes](../content-check-modes/README.md) |
| Update the database without downloading | `ofscraper metadata --metadata check` | [Metadata](../page/README.md) |
| Print what the database holds | `ofscraper db --usernames <creator>` | [Database Command](../page/database-command.md) |

## Options by topic

| Topic | Guide | Full list |
|---|---|---|
| Profile, config folder, site, env files, cache | [Advanced Args](../using-the-scraper/batch-scraping-and-bot-actions/advanced-args.md) | [Program Options](../reference/cli.md#program-options), [Advanced Program Options](../reference/cli.md#advanced-program-options) |
| Console, log file and Discord output | [Controlling Output/Logs](../getting-started/controlling-output.md) | [Logging Options](../reference/cli.md#logging-options) |
| Which creators, filters and sorting | [Model Filtering/Sorting](../using-the-scraper/batch-scraping-and-bot-actions/model-selection-sorting/README.md) | [User Selection Options](../reference/cli.md#user-selection-options), [User List Filter Options](../reference/cli.md#user-list-filter-options) |
| Post areas, dates, media and post filters | [Downloading Content](../using-the-scraper/batch-scraping-and-bot-actions/basic-actions/selecting-posts/README.md) | [Media Filters Options](../reference/cli.md#media-filters-options), [Posts Filters Options](../reference/cli.md#posts-filters-options) |
| File names | [Modifications to Filename](../using-the-scraper/batch-scraping-and-bot-actions/README.md#modifications-to-filename) | [Filename Modification Options](../reference/cli.md#filename-modification-options) |
| Download speed and resuming | [Performance Options](../getting-started/config-options/performance-options/README.md), [Download Options](../getting-started/config-options/download-options/README.md) | [Download Options](../reference/cli.md#download-options) |
| Scripts | [Script Options](../getting-started/config-options/script-options.md) | [Program Scripts](../reference/cli.md#program-scripts) |
| Daemon, actions, Fansly livestreams | [Basic Automation with command-line](../using-the-scraper/batch-scraping-and-bot-actions/README.md), [Fansly](../fansly.md#livestreams) | [Automation Options](../reference/cli.md#automation-options) |
| CDM key mode | [CDM Setup](../cdm-options/README.md) | [Advanced Program Options](../reference/cli.md#advanced-program-options) |

Run `ofscraper --help` or `ofscraper <subcommand> --help` to see the options your installed version accepts.
