# Enable label scan

## **what changed?**

Version 3.9 introduced a performance optimisation to `--posts all` by disabling label scans by default:

* In earlier versions, `--posts all` scanned labels to populate the `labels` table.
* While useful for some workflows, scanning labels can extend scan times if you don't need them in your database.
* Since version 3.9, labels are disabled by default with `--posts all`.

## adding labels to all

```sh
ofscraper --posts all,labels
```

## scraping just labels

```sh
ofscraper --posts labels
```

## shorthands for scraping all posts + labels

```sh
ofscraper --posts labels*
```

Or:

```sh
ofscraper --posts labels+
```

## permanently add labels to all

Set the environment default `OFSC_INCLUDE_LABELS_ALL` to `True`.

## repeat runs

Labels that have nothing new aren't paged through again. Check modes still scan labels in full.
