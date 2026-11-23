---
description: Control the detail level and display of program logs.
---

# Logging Options

## Log Levels

### -l, --log \[argument]

* **Sets:** The verbosity level for the program's log file.
* **Possible choices:**
  * `OFF`: Disables log file output.
  * `LOW`: Logs basic program flow and non-critical errors.
  * `NORMAL`: Logs most program activity and errors.
  * `DEBUG`: Logs all program activity and detailed debugging information.
  * `TRACE`: The most detailed log level.
* **Default:** Not set (the log level comes from `config.json`).

### -dc, --discord \[argument]

* **Sets:** The verbosity level for logs sent to Discord (if configured).
* **Possible choices:**
  * `OFF` (default): Disables Discord log output.
  * `LOW`: Sends basic program flow and non-critical errors to Discord.
  * `NORMAL`: Sends most program activity and errors to Discord.

### -p, --output \[argument]

* **Sets:** The verbosity level for log messages shown in the console.
* **Possible choices:**
  * `PROMPT`: Shows only critical information on the program prompt.
  * `LOW`: Shows basic program flow and non-critical errors.
  * `NORMAL` (default): Shows most program activity and errors.
  * `DEBUG`: Shows all program activity and detailed debugging information.

## Other Options

### -nl, --no-live-screen (also `--no-live`, `--no-rich`)

* **Controls:** Turns off Rich live displays (panels, spinners and progress bars).
* **Default:** `False`
