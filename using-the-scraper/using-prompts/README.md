---
description: Simplest way to run OF-Scraper
---

# Using Prompts

Running the prompt menu lets you use OF-Scraper with minimal arguments.

***

## Getting to the main menu

<figure><img src="../../.gitbook/assets/image (30).png" alt="" width="563"><figcaption></figcaption></figure>

The simplest method is to run:

```sh
ofscraper
```

Any command without `--action` opens this menu automatically.

***

> ℹ️ Some options open a submenu with a **Go to main menu** option.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt="" width="563"><figcaption></figcaption></figure>

***

## Action Menu

> ℹ️ **New in 3.7:** all scraping combinations can be run from this menu.

Use this menu to run scraping actions or combinations:

<figure><img src="../../.gitbook/assets/image (32).png" alt="" width="563"><figcaption></figcaption></figure>

**Browse and pick media (check table)** opens the check table for the creators you pick. See [Content Check Modes](../../content-check-modes/README.md).

***

## Going back and stopping

* **Esc** cancels the current prompt and returns to the menu it came from, changing nothing. On the main menu it does nothing.
* **Ctrl+C once** stops the current downloads, or the fetch of posts, messages, stories and other content, without quitting. From the menu you're taken back to the menu; a command-line run ends with exit code 130, and `--daemon` shuts down. Files that didn't finish keep their part files and resume on the next run.
* **Ctrl+C a second time** quits.
* A Fansly livestream recording is closed cleanly when stopped, so what was recorded is kept.

***

## Profile Menu

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt="" width="563"><figcaption></figcaption></figure>

Use this menu to:

* Add profiles
* Change the default profile
* Rename a profile
* Delete a profile

Each profile corresponds to a single account, so multiple accounts require multiple profiles.

***

## Edit config.json

<div align="center" data-full-width="false"><figure><img src="../../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure></div>

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

Use this menu to edit `config.json` directly from inside OF-Scraper without locating the file manually. Your existing settings are pre-filled so you can adjust them easily.

***

## Edit auth.json

> ℹ️ If authentication fails, the authentication menu pops up automatically and prompts you for new settings.

<figure><img src="../../.gitbook/assets/image (6).png" alt="" width="560"><figcaption></figcaption></figure>

You don't normally need to open this manually, though you can use it to edit `auth.json` directly.
