# Downloading Content

## Selecting Posts

### By post type

Pass a comma-separated list of post areas to download:

```sh
ofscraper --action download --posts highlights,timeline
```

Or repeat `--posts`:

```sh
ofscraper --action download --posts highlights --posts timeline
```

Duplicates are removed automatically.

### Options

* `profile`
* `highlights`
* `timeline`
* `archived`
* `stories`
* `messages`
* `purchased`
* `pinned`
* `streams`
* `labels`

#### Special Options

* `all`: scrapes `highlights`, `timeline`, `archived`, `stories`, `pinned`, `purchased`, `messages`, `profile`, and `streams` (labels require `labels`, `labels+`, or `labels*`)
* `labels*` or `labels+`: scrapes `all` plus `labels`

#### remove post type

Exclude a post type by prepending a hyphen (`-`), such as `-pinned`. This removes any selection, including from `all`. Hyphen exclusions only work with `--posts`, not with `--like-area` or `--download-area`.

***

## Bypass dupe check

By default, downloaded items are recorded in a database to prevent duplicate downloads. To download all available content for the current creator regardless, pass `--force-all`:

```sh
ofscraper --action download --force-all
```

***

## Filter Post by Date

> ℹ️ `X` must be a valid date.

### Before

Filters posts on or before the specified date. Works for downloading, liking, and unliking posts:

```sh
ofscraper --action download --before X
```

### After

Filters posts on or after the specified date. Works for downloading, liking, and unliking posts:

```sh
ofscraper --action download --after X
```

### **Valid Inputs**

> ℹ️ See the Arrow documentation for all supported input formats.

`YYYY-MM-DD, YYYY-M-DD, YYYY-M-D, YYYY/MM/DD, YYYY/M/DD, YYYY/M/D, YYYY.MM.DD, YYYY.M.DD, YYYY.M.D, YYYYMMDD, YYYY-DDDD, YYYYDDDD, YYYY-MM, YYYY/MM, YYYY.MM, YYYY, MM/DD/YYYY, M/D/YYYY`

`MM/DD/YYYY` and `M/D/YYYY` are accepted after the ISO formats, and the command-line help shows `MM/DD/YYYY` as the main format.

### Dehumanize Strings

Relative strings can be converted into dates using the form `<number> <timeframe> ago`.

**Timeframes:**

* `year`
* `month`
* `week`
* `day`
* `hour`
* `minute`
* `second`

Combine multiple timeframes with a comma for finer precision (when using debuggers, output displays in UTC):

```text
1 year ago, 1 month ago
```

***

## Filtering Timed Post (Promotional)

Skip all timed posts:

```sh
ofscraper --action download --skip-timed
```

### Filtering by text content

Accepts regex patterns (enclose the pattern in quotes to escape it properly). Including a capital letter enables case-sensitive matching.

#### Filter

Include only posts matching the regex pattern:

```sh
ofscraper --action download --filter X
```

#### Neg Filter:

Exclude posts matching the regex pattern (`--neg-filter` or `-nf`):

```sh
ofscraper --action download --neg-filter X
```

***

## Search entire paid page

Useful for situations such as when a creator's account has been deleted:

```sh
ofscraper --action download --scrape-paid
```

To scrape only the paid page and skip other prompts:

```sh
ofscraper --scrape-paid
```
