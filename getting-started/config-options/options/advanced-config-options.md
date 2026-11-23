# Advanced config options

## Contents

* [dynamic-mode-default](#dynamic-mode-default)
* [skip_unavailable_content](#skip_unavailable_content)
* [cache-mode](#cache-mode)
* [rotate\_logs](#rotate_logs)
* [sanitize\_text](#sanitize_text)
* [downloadbars](#downloadbars)
* [temp\_dir](#temp_dir)
* [infinite\_loop\_action\_mode](#infinite_loop_action_mode)
* [logs\_expire\_time](#logs_expire_time)
* [ssl\_verify](#ssl_verify)
* [incremental\_downloads](#incremental_downloads)
* [remove\_hash\_match](#remove_hash_match)
* [default\_user\_list](#default_user_list)
* [default\_black\_list](#default_black_list)
* [database\_url](#database_url)
* [env\_files](#env_files)
* [Environment variables](#environment-variables)

***

***

## dynamic-mode-default

Default: `digital`

* Used to sign requests for authorisation. Without it, requests fail authorisation.
* The options behave mostly the same, though switching options can occasionally resolve authentication issues.

**Accepted values:**

* `datawhores`, `xagler`, `rafa`
* `digitalcriminals` (also written `digital`, `dc`, `digitals`, or `digitalcriminal`; the config menu saves it as `digital`)
* `generic` (needs `OFSC_DYNAMIC_GENERIC_URL`) and `manual` (needs `OFSC_DYNAMIC_RULE_MANUAL`)
* `dv` and `dev` are removed.
* An unknown value falls back to the default with a warning in the log.

***

## skip_unavailable_content

* Bypasses the Timeline, Pinned, Archived, Labels, Stories, and Highlights API endpoints for expired creators within a grace period (default: 1 day).
* Continues to scan Messages, Purchased, and Profile content.

***

## cache-mode

> ℹ️ If you're having cache issues, you can pass `--no-cache` or `--no-api-cache`.

**Options** (default `sqlite`):

* `sqlite`
* `json`
* `disabled`: no cache, no API cache, and no incremental downloads (like `--no-cache`).
* `api_disabled`: no API response cache only (like `--no-api-cache`).

OF-Scraper uses DiskCache, which supports SQLite and JSON backends. SQLite works well for most setups, but if your config is on a network drive, switching to JSON can improve performance. See [DiskCache caveats](https://grantjenks.com/docs/diskcache/tutorial.html#caveats).

***

## rotate\_logs

When `true`, each run creates a new log file. When `false`, logs are combined into one file per day.

## sanitize\_text

When `true`, text content is sanitised before insertion into the database.

## downloadbars

Controls whether to show download progress bars. Disabling them can improve performance.

***

## temp\_dir

Overrides the temporary directory used during downloads.

> ℹ️ If not set, the final download directory is used to hold temporary files.

## infinite\_loop\_action\_mode

Runs the scraper in an infinite loop even when `--action` is used.

> ℹ️ You can disable the prompt for continuing with arguments by setting the `OFSC_CONTINUE_BOOL` environment variable to `false`.

## logs\_expire\_time

Maximum age for log files in hours. When `rotate_logs` is enabled and this value is greater than `0`, log files older than this limit are deleted automatically.

***

## ssl\_verify

Controls how the scraper handles SSL certificate validation and TLS fingerprinting.

**Available options:**

* `"custom"` **(Default & recommended):** uses a custom SSL context with TLS fingerprint hardening.
* `"default"`: uses standard Python SSL validation (the default behaviour of `aiohttp`).
* `"false"`: disables SSL certificate validation entirely.

***

## incremental\_downloads

> ℹ️ Replaces `auto_after`.

* Default `true`. When `true` and no `--after` is given, each area is scanned only from the newest previously scanned post.
* Like/unlike actions and forced full scans still scan everything.
* Turned off for the run by `--no-cache` or `cache-mode` set to `disabled`.
* The old `enable_auto_after` key is still read if this key is missing.

***

## remove\_hash\_match

If at least two files with identical hashes exist on the system, removes duplicate files and keeps only one copy on disk.

> ℹ️ Set to `null` to disable hash calculation. `false` calculates hashes without removing files.

> ℹ️ Hashes are 128-bit and matched alongside file sizes to ensure uniqueness.

***

> ℹ️ **Built-in list keywords:**
> * `ofscraper.main` or `main`: combines active and expired lists.
> * `ofscraper.active` or `active`: active list.
> * `ofscraper.expired` or `expired`: expired list.

## default\_user\_list

The default user list used during username scans.

> ℹ️ If blank, `ofscraper.main` is used.

## default\_black\_list

The default blacklist used during username scans.

> ℹ️ If blank, the blacklist option is disabled.

***

## database\_url

Since 3.18.0. Not a setting: it only says that the PostgreSQL address is set with the `OFSC_DATABASE_URL` environment variable, which is kept out of `config.json` because it holds a password. Anything written here is ignored and replaced, with a warning. See [PostgreSQL](../../../page/postgresql.md).

***

## env\_files

List of files imported to set custom environment variables (`OFSC_*` overrides). Later files override earlier ones. Environment variables apply at runtime only and aren't saved into `config.json`.

***

## Environment variables

Environment variables let advanced users control additional settings in OF-Scraper.

**Default values:** All environment variable keys are listed under `ofscraper/utils/of_env/values`, grouped into separate folders and files by type. Each default can be overridden with its `OFSC_<NAME>` variable (for example `OFSC_DISCORD_ASYNC`), or with the bare key name. Every key is in [Environment defaults](../../../reference/env.md).

> ℹ️ **Environment variables only change built-in defaults.** They don't override a value that is set in `config.json`.

### Configuration Precedence

When resolving a configuration setting, OF-Scraper checks these sources in order. Higher items **override** lower ones:

1. **Explicit `.env` file (`--env-files` option, or `advanced_options.env_files` in `config.json`):** Loads values from the specified `.env` file(s). When `--env-files` is used, it replaces `advanced_options.env_files`. If `--env-files` is passed multiple times (e.g. `ofscraper --env-files a.env --env-files b.env`), files are loaded in the order given, and later files take precedence over earlier ones and over the sources below.
2. **Automatic `.env` file (via `load_dotenv()`):** Loads a default `.env` file. Searches upward from the program's install folder (from the working folder instead, in standalone binaries).
3. **System environment variables:** Values already set in your OS environment (e.g. `export VAR=VALUE` on Linux/macOS, or `set VAR=VALUE` on Windows Command Prompt), present before any `.env` files are loaded.
4. **Hardcoded defaults:** Default values defined in the source code, used only if a setting isn't found in any source above.
