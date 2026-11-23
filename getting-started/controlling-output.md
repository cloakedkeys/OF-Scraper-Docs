---
description: various options for output
---

# Controlling Output/Logs

***

## Log Streams

### Discord

Sends output to your Discord channel.

> ℹ️ Discord logs contain only the log message, whereas other logs include additional details like function calls and line numbers.

> ℹ️ You can set the environment default `OFSC_DISCORD_ASYNC` to `true` to speed up Discord logs, though messages may arrive out of order.

> ℹ️ Discord accepts only `OFF`, `LOW`, and `NORMAL` (`NORMAL` is its highest level).

#### LEVELS

*In ascending output order:*

* `OFF`
* `LOW`
* `NORMAL`

***

### Output

Outputs to the console.

> ℹ️ For clear console output, set the logging level to `NORMAL` or lower to avoid excessive messages.

#### LEVELS

*In ascending output order:*

* `PROMPT`
* `LOW`
* `NORMAL`
* `DEBUG`

***

### Log

Outputs to a log file in the config folder (`~/.config/ofscraper/logging/`).

*In ascending output order:*

* `OFF`
* `LOW`
* `NORMAL`
* `DEBUG`
* `TRACE`

Removed:

* `STATS`

***

> ℹ️ **Logs are safe to share after a check:** the OnlyFans session cookie and the Fansly token are masked in log lines. Still look for personal details before posting a log.

## Log levels details

With the 1.9 release, you have finer control over each output level:

| Level | Description |
|---|---|
| `OFF` | Disables Discord or log file logging. Default for Discord (the log file defaults to `DEBUG`). |
| `PROMPT` | Shows only prompts and essential console output. Passing a scraping action and usernames disables most or all additional output. |
| `LOW` | Disables all progress bars and displays essential program status while running (including avatars). Applies to all output destinations. |
| `STATS` | *(Removed in 3.5.)* Slight modification to `LOW` with no avatars shown. |
| `NORMAL` | Default console output level. Shows progress bars and general status messages on the console; Discord and log files receive general status messages without progress bars. |
| `DEBUG` | Adds debugger messages and tracebacks on top of `NORMAL`. Applies to console and log file only. |
| `TRACE` | *(Log file only.)* Provides the most detailed output of all modes. |
