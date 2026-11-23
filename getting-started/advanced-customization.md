# Advanced Configuration

Environment variables let advanced users control additional settings in OF-Scraper.

**Default values:** All environment variable keys are listed under `ofscraper/utils/of_env/values`, grouped into separate folders and files by type. Each default can be overridden with its `OFSC_<NAME>` variable (for example `OFSC_DISCORD_ASYNC`), or with the bare key name.

> ℹ️ **Environment variables only change built-in defaults.** They don't override a value that is set in `config.json`.

#### Configuration Precedence

When resolving a configuration setting, OF-Scraper checks these sources in order. Higher items **override** lower ones:

***

1. **Explicit `.env` file (`--env-files` option, or `advanced_options.env_files` in `config.json`):** Loads values from the specified `.env` file(s). When `--env-files` is used, it replaces `advanced_options.env_files`. If `--env-files` is passed multiple times (e.g. `ofscraper --env-files a.env --env-files b.env`), files are loaded in the order given, and later files take precedence over earlier ones and over the sources below.
2. **Automatic `.env` file (via `load_dotenv()`):** Loads a default `.env` file. Searches upward from the program's install folder (from the working folder instead, in standalone binaries).
3. **System environment variables:** Values already set in your OS environment (e.g. `export VAR=VALUE` on Linux/macOS, or `set VAR=VALUE` on Windows Command Prompt), present before any `.env` files are loaded.
4. **Hardcoded defaults:** Default values defined in the source code, used only if a setting isn't found in any source above.
