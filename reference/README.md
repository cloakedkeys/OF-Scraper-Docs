---
description: Every option, setting, default and database table, in one place.
---

# Technical Reference

The rest of these docs show you how to use OF-Scraper. This section is for when you need the exact details: what a setting is called, what its default is, and what else it affects.

The list pages are built from the code itself, so they match what the program actually does. The hooks page is written by hand and checked against the code.

## Pick a page

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody>
<tr><td><strong>⌨️ Command-line options</strong></td><td>Every command and option you can type, with its default and the <code>config.json</code> setting it replaces.</td><td><a href="cli.md">cli.md</a></td></tr>
<tr><td><strong>⚙️ config.json keys</strong></td><td>Every setting in <code>config.json</code>: what it does, its default, and older names that still work.</td><td><a href="config.md">config.md</a></td></tr>
<tr><td><strong>🌱 Environment defaults</strong></td><td>Built-in limits, timeouts and retry settings, and the environment variables that change them.</td><td><a href="env.md">env.md</a></td></tr>
<tr><td><strong>🏷️ Placeholders</strong></td><td>The <code>{names}</code> you can use to build folder and file names.</td><td><a href="placeholders.md">placeholders.md</a></td></tr>
<tr><td><strong>🗄️ Database tables</strong></td><td>What OF-Scraper remembers about each creator, and what writes each record.</td><td><a href="database.md">database.md</a></td></tr>
<tr><td><strong>🧭 How settings and files work</strong></td><td>Which setting wins, which files get written, and where everything is saved.</td><td><a href="how-it-works.md">how-it-works.md</a></td></tr>
<tr><td><strong>🧩 Hooks for add-ons</strong></td><td>Functions and events that code such as the GUI patch can use instead of copies of the scraper's files.</td><td><a href="hooks.md">hooks.md</a></td></tr>
<tr><td><strong>🧪 Testing</strong></td><td>How to install the test dependencies and run the test suite from a clone.</td><td><a href="testing.md">testing.md</a></td></tr>
</tbody></table>

## Common questions

**I changed `config.json` but nothing changed.**
A command-line option overrides the same setting in `config.json`. See [which setting wins](how-it-works.md#where-a-settings-value-comes-from).

**How do I change where files are saved or what they're called?**
Set `file_options.save_location`, `dir_format` and `file_format` in [config.json](config.md), using the [placeholders](placeholders.md).

**Where are my config, logs and database?**
See the [default folder layout](how-it-works.md#default-folder-layout).

**Downloads are slow or keep getting rate-limited.**
The retry and wait times are in [Rate-limit & backoff settings](env-ratelimits.md).

**What does this fork add?**
See [Fork Changes](../fork-changes.md), or the short list in [Features added since 3.14.7](how-it-works.md#features-added-since-3.14.7).
