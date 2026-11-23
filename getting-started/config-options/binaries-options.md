---
description: Required Binaries for protected downloads
---

# Binaries Options

## ffmpeg

`ffmpeg` decrypts protected videos and combines their audio and video parts into the final output file.

### Version and lookup

> ℹ️ **Since 3.15.0.** 3.14.7 and earlier reject `ffmpeg` 8 and newer, and treat a quoted or empty path as a real value. See [Fork Changes](../../fork-changes.md).

* **Version:** `ffmpeg` **6 or newer**. 8.x and 9.x are accepted; versions below 6 are rejected.
* **Lookup order:** the `ffmpeg` config path (or the `OFSC_FFMPEG_DEFAULT` environment variable when the setting is empty), then the `pyffmpeg` binary, then `ffmpeg` on your `PATH`. Each must pass the version check.
* **Empty setting:** `"ffmpeg": ""` counts as unset, so `OFSC_FFMPEG_DEFAULT` and the fallbacks above apply.
* **Quoted paths:** a path pasted with surrounding quotes (Windows' "Copy as path") is accepted.
* **Docker:** amd64 uses `pyffmpeg`'s `ffmpeg`, and arm64 ships a static `ffmpeg` 9.0.2.

### Download Sources

* [BtbN FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds/releases)
* [FFmpeg Downloads](https://ffmpeg.org/download.html)

### Releases

#### **Windows**

[https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-win64-gpl-shared.zip](https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-win64-gpl-shared.zip)

#### **Linux**

[https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-linux64-gpl-shared.tar.xz](https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-linux64-gpl-shared.tar.xz)

#### Mac

> ℹ️ The latest snapshot is recommended.

[https://evermeet.cx/ffmpeg/get/zip](https://evermeet.cx/ffmpeg/get/zip)
