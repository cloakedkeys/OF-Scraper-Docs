# Downloading Text Files

> ℹ️ Text files are handled differently because there are no text media uploads; instead, they're based on posts and tied to multiple media.

There is no `config.json` setting for text files (`--mediatypes` / `-mt` and `config.json`'s `filter` only accept `Videos`, `Audios`, and `Images`). Use these command-line options instead:

* `--text` (also `-t`, `--download-text`): downloads text files alongside media.
* `--text-only` (also `-tx`, `--download-text-only`): downloads only text files and skips all media.

Notes:

* On the content-check and manual commands, `--text` and `--text-only` can't be used together, and their short forms are `-tn` (`--text`) and `-tp` (`--text-only`) instead of `-t` and `-tx`.
* Text files are only written by the `download` action, not by `like` or `unlike`.
