---
description: Download media from specific URLs or post IDs without using user lists.
---

# Manual Mode Options

## Syntax

```
ofscraper manual [options]
```

### Example

```
ofscraper manual --url test
```

## General Options

See [General Program Options](shared-options/common-option-groups/).

## Text

### -tn, --text

* Downloads text alongside any media tied to that text.

### -tp, --text-only

* Downloads only text, skipping media.

`--text` and `--text-only` can't be used together.

## Download Sources

Use either `-f` or `-u`, not both. Exactly one is required.

### -f, --file \[argument]

Downloads media from a file containing URLs or post IDs, one per line.

### -u, --url \[argument]

Downloads media directly from one or more URLs (separated by spaces or commas).

### -fo, --force

Forces fresh retrieval of post information from the API.
