# Creating Metadata

Metadata is automatically created when you download data. The tables and their structure are determined by the API you're using and the version of OF-Scraper you're running.

## metadata mode

> ℹ️ You can use `--anon` to gather metadata without logging in, though you lose access to most media data.

Enter metadata mode with the `metadata` subcommand:

```sh
ofscraper metadata [args]
```

This updates metadata without downloading files. Existing stories are updated too, not just new ones, and messages keep their deleted flag.

* [Shared Scrape and Metadata Check Mode Options](../command-reference/shared-options/scrape-metadata-options/)
* [Metadata Check Mode Options](../command-reference/metadata-check-mode-options.md)
