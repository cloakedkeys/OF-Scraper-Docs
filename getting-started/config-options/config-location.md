# Config Location

### Config Path

The config file is `.config/ofscraper/config.json` under the user's home folder on every OS.

#### Windows

```text
C:/Users/<username>/.config/ofscraper/config.json
```

#### Linux

```text
/home/<username>/.config/ofscraper/config.json
```

> ℹ️ **Running with `sudo` or as `root`:** the file is located at `/root/.config/ofscraper/config.json`.

#### macOS

```text
/Users/<username>/.config/ofscraper/config.json
```

If no `config.json` exists, a new one is written from the built-in defaults.

#### Change config location

You can change the config location with `OFSC_CONFIG_DIR` (a folder relative to the home folder, default `.config/ofscraper`) or the `--config` option. See [Advanced Args](../../using-the-scraper/batch-scraping-and-bot-actions/advanced-args.md).
