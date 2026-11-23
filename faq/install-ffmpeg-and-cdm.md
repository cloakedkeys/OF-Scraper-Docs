# Install, FFmpeg & CDM

## ofscraper not found

This usually means you need to add the install folder to your `PATH`.

***

## FFMPEG

`ffmpeg` 6 or newer is required for downloading protected content. See [FFmpeg Downloads](https://ffmpeg.org/download.html).

#### Binaries

> ℹ️ If you download `ffmpeg` manually, put its full path in `config.json`.

See [Binaries Options](../getting-started/config-options/binaries-options.md).

<details>

<summary>Copying a path on Windows</summary>

If Windows doesn't give you an easy way to copy a file path, you can use [Path Copy Copy](https://pathcopycopy.github.io/).

</details>

***

## ffmpeg isn't found even though it's installed

Put the full path to the `ffmpeg` program in `binary_options` → `ffmpeg` in your config, for example `C:\ffmpeg\bin\ffmpeg.exe`. An empty setting means "not set".

***

## FFmpeg shared library not found Error

Example: ``version `GLIBCXX_3.4.29' not found``

### Cause

Missing shared libraries (Linux only).

### Fix

Use the GPL non-shared release build from [BtbN FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds/releases).

### Some Info

* [Which version of ffmpeg is the latest? (Super User)](https://superuser.com/questions/1712179/which-version-of-ffmpeg-is-the-latest)
* The version in your Linux distribution's repository may not work.

***

## CDM Issues

See [CDM issues](../cdm-options/cdm-issues.md).

***

## It says to update to 3.14.7

3.14.7 is the last of upstream's old `ofscraper` releases on PyPI, and it's older than this fork's code. Version 3.15.0 and later no longer show that message. From 3.16.2 the update check looks up `ofscraper-community`; from 3.17.0 it looks up the package you installed (`ofscraper-community`, or `ofscraper`, which `datawhores/OF-Scraper` now publishes from the same code).
