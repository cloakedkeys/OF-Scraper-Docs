---
description: Options for the content check subcommands (post_check, msg_check, paid_check and story_check).
---

# Content Check Modes Options

> ℹ️ **Cached information is generally stored for around 3 days to improve efficiency.**

## Syntax

```
ofscraper [subcommand_name] [subcommand_options]
```

### Example

```
ofscraper post_check --url test
```

## General Options

See [General Program Options](shared-options/common-option-groups/).

## Subcommand Options

Each content check subcommand (`post_check`, `msg_check`, `paid_check`, `story_check`) accepts common arguments for choosing content sources and controlling update behaviour.

### Specifying Content Source

One of `-u` or `-f` is required.

* **`-u, --url [argument]`** (`post_check`, `msg_check`):
  * Scans content from one or more URLs (separated by spaces or commas). `post_check` also accepts bare usernames.
  * `msg_check` also accepts a creator username, or any text containing a number, which is taken as the model ID (for example, a chat URL).
* **`-u, --usernames [argument]`** (`story_check`, `paid_check`):
  * Scans content from one or more usernames (`paid_check` also accepts a user ID).
* **`-f, --file [argument]`** (all subcommands):
  * Scans content from a file with one entry per line. For `post_check` and `msg_check` the entries are URLs (or usernames, as above); for `story_check` and `paid_check` they are usernames.

### Forcing Update

* **`-fo, --force`** (`post_check`, `msg_check`, `paid_check`, `story_check`):
  * **Default:** `False` (uses cached data if available).
  * Forces the API to fetch the latest information, bypassing the cache.

### Text

#### -tn, --text

* Downloads text alongside any media tied to that text.
* Available in `post_check`, `msg_check` and `paid_check` (not `story_check`).

#### -tp, --text-only

* Downloads only text, skipping media.
* Available in `post_check`, `msg_check` and `paid_check` (not `story_check`).

`--text` and `--text-only` can't be used together.

### Post areas (`post_check` only)

* **`-ca, --check-area [argument]`:** Areas to check: `all`, `archived`, `timeline`, `pinned`, `labels`, `streams`. Several can be given, separated by spaces. Default: `timeline`, `pinned`, `archived` and `streams`. Also `--post`, `--posts`.
* **`-tls, --timeline-strict`:** When `timeline` is selected, removes pinned and archived posts.

### Table filters

Each check subcommand also has its own table filters: `-ucl, --unlocked` or `-lc, --locked`, `-dwl, --downloaded` or `-ndw, --not-downloaded`, `-pf, --posted-after`, `-pb, --posted-before`, `-mid, --media-id`, `-pd, --post-id`, `-to, --protected-only` or `-no, --normal-only`, `-lx, --length-max`, `-lm, --length-min`, `-mt, --mediatype`, `-mdc, --media-desc`, `-sm, --size-min` and `-sx, --size-max`. Run `ofscraper <subcommand> --help` for the full list.

`-mst, --media-sort` here takes `number`, `username`, `downloaded`, `unlocked`, `length`, `mediatype`, `post_date`, `post_media_count`, `responsetype`, `price`, `post_id`, `media_id` or `text`.

> ℹ️ **Fork:** `msg_check` has its own `--help`, and bad command-line input prints a short usage message. A failed run exits with status 1.

## Subcommand Descriptions

* **`post_check`:** Analyses posts from URLs or a file and displays them in a table.
* **`msg_check`:** Analyses messages from URLs or a file and displays them in a table.
* **`paid_check`:** Analyses purchased content from usernames or a file and displays it in a table.
* **`story_check`:** Analyses stories and highlights from usernames or a file and displays them in a table.

