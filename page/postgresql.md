---
description: Keep every creator's database in one PostgreSQL database
---

# PostgreSQL

By default OF-Scraper keeps one SQLite file (`user_data.db`) per creator. Nothing needs installing, and that stays the default.

As an option, it can keep every creator's rows in one PostgreSQL database instead. That is useful if you want one place to query and back up, or you run the scraper from more than one machine against the same library.

> ℹ️ **In releases after 3.17.1.** Before such a release is out, install from GitHub (see below).

This page covers what you need to use it. [POSTGRESQL.md](https://github.com/cloakedkeys/OF-Scraper-Community/blob/main/POSTGRESQL.md) in the fork has every detail.

***

## What you need

* A PostgreSQL server, version 15 or newer, and a database on it that the scraper's login may create tables in.
* The PostgreSQL driver:
  * **pip:** `pip install "ofscraper-community[postgres]"`, in releases after 3.17.1. Before such a release is out, install from GitHub: `pip install "ofscraper-community[postgres] @ git+https://github.com/cloakedkeys/OF-Scraper-Community"`.
  * **Docker:** the image already includes it.
  * **Binary releases** (the `.exe` and the other single files) don't include it. Use the pip or Docker install.

## Turning it on

Set `OFSC_DATABASE_URL` to the database's address:

```text
OFSC_DATABASE_URL=postgresql://user:password@host:5432/database
```

* Set it as an environment variable (in `docker-compose.yml`, under `environment:`), or as a line in a `.env` file that [`env_files`](../getting-started/config-options/options/advanced-config-options.md#env_files) names.
* Leave it unset, or empty, to keep using SQLite files.
* It isn't a `config.json` setting, because it holds a password. `advanced_options.database_url` in `config.json` only points here; anything written there is ignored.
* The password is never written to the log. If a special character in it breaks the address, percent-encode it (`@` is `%40`).

At startup the scraper connects once and says which server it is using. If it can't, it stops there with one sentence saying why.

## Bringing your existing databases in

Turning PostgreSQL on doesn't move what your `user_data.db` files hold. Until you bring them in, the scraper treats everything as new and downloads it again. Where an identical file is already at the same path, it's kept and the new copy is dropped (not with allow-dupes on).

```sh
python -m ofscraper.commands.postgres_import <folder>
```

* `<folder>` is searched for `user_data.db` files. Your profile's `.data` folder is the usual one.
* Run like that, it only reports what it found. Add `--apply` to bring the files in.
* Your files are never changed, and it's all or nothing: if anything fails, PostgreSQL keeps none of it.
* If two files hold the same creator, put them together with Merge Databases first.
* Don't run the scraper while it runs.

Afterwards the `user_data.db` files are no longer used. Keep them as your copy from before the switch.

## Going back to SQLite files

Unsetting `OFSC_DATABASE_URL` returns to your old `user_data.db` files, without anything scraped since. To write what PostgreSQL holds back to files first:

```sh
python -m ofscraper.commands.postgres_export <folder>
```

* Each creator gets `<folder>/<creator id>/user_data.db`.
* Run like that, it only reports. Add `--apply` to write the files.
* PostgreSQL is only read, and a file that is already there is never changed.
* If PostgreSQL has rows for both OnlyFans and Fansly, add `--site onlyfans` or `--site fansly` and give each site its own folder.

## Tools that run on their own

`stash_sync`, `recover_collisions`, `move_creator_files` and `scripts/creator_names.py` work on PostgreSQL when you add `--postgres`. They find it only through `OFSC_DATABASE_URL` in the environment they are run in, not through the scraper's `env_files`. See [Organize Downloads in Stash](../using-the-scraper/recipes/stash.md), [Recover Filename Collisions](../using-the-scraper/recipes/recover-filename-collisions.md) for each tool, and [POSTGRESQL.md](https://github.com/cloakedkeys/OF-Scraper-Community/blob/main/POSTGRESQL.md) for its `--postgres` options.

## What is different

* **One database for every creator and every profile.** Each site has its own schema (`onlyfans`, `fansly`). Switching profiles doesn't switch the data, and the scraper says so when you switch.
* **Already-downloaded media is still judged per creator**, as with the files.
* **No automatic backup copies.** Back up with `pg_dump`.
* **Your SQLite files are left alone** while PostgreSQL is on.

## What doesn't use it yet

* **Merge Databases** works on `user_data.db` files only, and says so on its screen.
* **The GUI patch:** scraping, downloads, metadata updates and the check tables go through the scraper, so they use PostgreSQL. Its results table, purge and "new since last run" read the `user_data.db` files themselves, so they see only the old files. Developers: [Hooks for add-ons](../reference/hooks.md) lists the reads the GUI can use instead.
