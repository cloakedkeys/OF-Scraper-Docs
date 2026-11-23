# General Options

***

## main\_profile

> ℹ️ All profiles share the same configuration unless overridden with `--config`.

> ℹ️ To use multiple profiles, pass `--profile`.

* In most cases, there's no need to change this setting. Profiles are organised into directories inside the config location, named after the profile.
* Each directory can hold its own authentication file.

***

## discord

To send updates to Discord using webhooks, follow Discord's [Intro to Webhooks](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks) guide.

Add the webhook URL to `discord` in `config.json`, and raise the Discord log level with `-dc` / `--discord` `LOW` or `NORMAL` (default `OFF`). Nothing is sent while it stays `OFF`.

***

## New config files and environment variables

* A new `config.json` is written from the built-in defaults.
* Environment variables (`OFSC_*`) apply at runtime only and aren't saved into `config.json`.
