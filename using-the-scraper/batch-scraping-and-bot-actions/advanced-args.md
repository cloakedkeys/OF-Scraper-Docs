# Advanced Args

***

### --profile

Can be combined with `--config`. Takes precedence over the active profile in `config.json`. Without it, the profile in `main_profile` in `config.json` is used (also called `main_profile` unless you change it). For example, `-r test` uses a profile named `test`.

***

### --site

Picks the site for this run: `onlyfans` or `fansly`. Without it, the profile's `site.json` decides, and OnlyFans is the default:

```sh
ofscraper --site fansly
```

***

### --env-files

Loads environment variables from a file (`.env`, `.yaml`/`.yml` or `.json`). Can be given more than once; later files override earlier ones. It replaces the `env_files` setting in `config.json` instead of adding to it. See [Environment variables](../../getting-started/config-options/options/advanced-config-options.md#environment-variables).

```sh
ofscraper --env-files /path/to/prod.env
```

***

### --users-first

Changes the download order to fetch links for all selected creators first before starting downloads. Downloads may take longer to begin, but this can be useful in some setups (`--user-first`, `-uf`, `--usersfirst`, and `--userfirst` also work):

```sh
ofscraper --users-first
```

***

### --username-individual-search and --username-list-search

These set how the creators given with `--username` are looked up:

* `--username-individual-search` (`-fi`) looks up each username in a separate request. This can be faster than fetching the lists, but many requests can hit rate limits.
* `--username-list-search` (`-fl`) fetches the whole enabled user list (`default_user_list` in `config.json`, or `--user-list`) and picks the usernames from it. Useful for a large number of users.

Without either, the choice depends on how many usernames you give and how many subscriptions the account has.

***

### multiple configs

```sh
ofscraper --config <folder or file>
```

OF-Scraper checks the locations below in order and stops at the first match (or uses the fallback):

| Check | Config file | Config folder |
|---|---|---|
| `--config` isn't passed | `$HOME/.config/ofscraper/config.json` | `$HOME/.config/ofscraper/` |
| `config_arg` is an existing file | `config_arg` | Parent directory of `config_arg` |
| `config_arg` is an existing directory | `config_arg/config.json` | `config_arg` |
| `config_arg` has no extension | `config_arg/config.json` | `config_arg` |
| `config_arg` is just a filename (e.g. `test.json`) | `$HOME/.config/ofscraper/config_arg` | `$HOME/.config/ofscraper` |
| Fallback (always true; the only remaining case is a full file path such as `/home/me/test.json`) | `config_arg` | Parent directory of `config_arg` |

#### Shared information

Two configs in the same folder can share:

* Profiles
* Log files
* Cache
* Authorisation

#### Duplication check

This depends on your config settings. Configs with identical metadata settings don't download duplicates of each other.

***

### multiple profile auth

Authentication for different accounts is managed through profiles. Change the active profile in `config.json` or with `--profile`:

#### Example

```sh
ofscraper --profile test
```

With config file location `/home/test/.config/ofscraper/config.json`, the profile is always inside the config file's parent folder with `_profile` appended:

```text
/home/test/.config/ofscraper/test_profile
```

***

### --no-cache

Disables all caching (such as stored keys and file sizes) and stops reading previously cached data.

As a result, API requests run synchronously (each request finishes before the next begins), because concurrent API processing relies on cached data. This also disables caching for decryption key retrieval.

```sh
ofscraper --no-cache
```

### --no-api-cache

Like `--no-cache`, but disables caching and cached data reads for API calls only.

As a result, API requests run synchronously (each request finishes before the next begins), because concurrent API processing relies on cached data.

```sh
ofscraper --no-api-cache
```

***

### --update-profile

Profile information is cached for about a day. `--update-profile` (`-up`) fetches it from the API instead of the cache.

### --auth-fail

`--auth-fail` (`-al`, also `--auth-quit`) quits when authentication fails, instead of prompting for new details.
