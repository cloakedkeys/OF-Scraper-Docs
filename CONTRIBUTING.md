# Editing these docs

These pages are published to GitBook through Git Sync. `SUMMARY.md` sets the sidebar; a page that isn't listed there isn't shown.

* **Generated pages in `reference/`** (`cli.md`, `config.md`, `env.md`, `placeholders.md`, `database.md`) are copied from the fork. Don't edit them here. To refresh them, run and commit the result:
  ```sh
  python scripts/sync_reference.py <path to the fork checkout>
  ```
* **Hand-written reference pages:** `reference/README.md` and `reference/how-it-works.md` are written by hand here.
* **`reference/hooks.md`** is copied by hand from the fork's `reference/hooks.md`. Change it in the fork first, then update its fork-file links to GitHub links and convert its in-page links to GitBook anchors (lower-cased, dots kept, backticks and a trailing bracket dropped, and each run of other punctuation or spaces turned into one `-`, so `gather_rows(command)` becomes `#gather_rows-command` and `Features added since 3.14.7` becomes `#features-added-since-3.14.7`).
