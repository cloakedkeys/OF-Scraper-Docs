---
description: Requirements for uv or pip installations
---

# Requirements

> ℹ️ **cloakedkeys fork: Python 3.11 to 3.15 are supported** (CI tests on 3.11 and 3.15.2). On 3.15, `lz4` and `faust-cchardet` have no prebuilt wheels and build from source, so a C compiler is needed (MSVC on Windows). Docker images and release binaries use 3.15.1.

> ℹ️ **DRM downloads need `ffmpeg` 6 or newer.** 8.x and 9.x work. Fansly livestream recording and streamed videos also use `ffmpeg`. See [Binaries Options](getting-started/config-options/binaries-options.md).

The notes below are from upstream:

* Python 3.11 is compatible with most versions.
* Python `<=3.10` is compatible with some older versions.
* Python `>=3.13` is compatible with 3.7 and beyond.
