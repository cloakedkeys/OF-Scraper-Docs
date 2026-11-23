---
description: Options that control the program's general behaviour.
---

# Program Options

## General Options

### -v, --version

* **Displays:** The program's version number, then exits.
* **Example output:** `2.4.5+main.8f998cd` (varies by version).

### -cg, --config \[argument]

* **Controls:** The location of the configuration folder or file.
* **Default:** Uses the default configuration location.
* **Example:** `-cg /custom/config/path` looks for configuration files in `/custom/config/path`.

See [Advanced Args](../../../using-the-scraper/batch-scraping-and-bot-actions/advanced-args.md).

### -r, --profile \[argument] (optional)

* **Specifies:** The name of the profile directory inside the config location, which stores authentication information.
* **Default:** The profile set in `config.json` under `main_profile` (also called `main_profile` unless you change it).
* **Example:** `-r test` uses a profile named `test`.

### --site \[onlyfans|fansly]

* **Specifies:** The site to use for this run.
* **Default:** If not set, the profile's `site.json` decides, and OnlyFans is the default.
* **Example:** `--site fansly` uses Fansly for this run.

### --env-files \[path]

* **Specifies:** The path to an external environment file (`.env`, `.yaml`/`.yml` or `.json`) to load environment variables from. Can be given more than once.
* **Effect:** Loads variables from the file into the program's environment, overriding any matching system environment variables. If several files are given, later files override earlier ones. Settings that read from environment variables then use those values.
* **Default:** If not provided, the `env_files` setting in `config.json` is used instead (not in addition).
* **Example:** `--env-files /home/user/my_app/prod.env` loads environment variables from `prod.env`.

See [Advanced Customization](../../../getting-started/advanced-customization.md).
