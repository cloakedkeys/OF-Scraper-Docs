---
description: >-
  This page provides an overview of the different release types, versioning, and
  file formats for OF-Scraper.
---

# Release Info

## Release Types

OF-Scraper uses three release types to indicate stability and origin.

### Continuous Development Builds (Snapshot Releases)

Generated directly from recent commits on development branches (like `main`). They reflect the latest state of the codebase and include a commit hash in their name.

* **Naming convention:** Includes the version, a short commit hash, and the **date of the associated commit for chronological sorting** (e.g. `3.17.1-9e54ed3-1749940070`).
* **Stability:** Bleeding-edge; may contain new features, bug fixes, or unresolved issues. Intended for testing and development.
* **Example tag:** `3.17.1-9e54ed3-1749940070`

### Pre-release Versions (e.g., `X.Y.Z.devN`)

Semi-stable builds pushed for broader testing before a stable release.

* **Naming convention:** `major.minor.patch.devN` (e.g. `3.7.0.dev0`).
* **Stability:** More stable than continuous development builds, but still under testing.
* **Example version:** `3.7.0.dev0`

### Stable Releases (Numbered)

Tested, production-ready releases for general use.

* **Naming convention:** Standard semantic versioning (`X.Y.Z`, e.g. `3.6.0`).
* **Stability:** Highly stable and recommended for most users.
* **Example version:** `3.6.0`

***

## Release Distributions

### Python Package

This fork is published to PyPI as **`ofscraper-community`**, starting with 3.16.2. The command is still `ofscraper`. (`datawhores/OF-Scraper` also publishes this same code as `ofscraper`; versions `3.14.7` and older are upstream's old code without the fork's fixes.) See [UV Install](uv-install.md).

- [ofscraper-community on PyPI](https://pypi.org/project/ofscraper-community/)

### Docker Images

Multi-arch Docker images are hosted on [GitHub Container Registry](https://github.com/cloakedkeys/OF-Scraper-Community/pkgs/container/of-scraper-community).

### Binaries

Each release includes standalone binaries on [GitHub Releases](https://github.com/cloakedkeys/OF-Scraper-Community/releases) for Windows, macOS, and Linux.

#### Release Files

Binaries are provided in formats compatible with each platform.

#### Example Files

Typical files attached to a release:

* `ofscraper_windows_3_16_1.exe` (Windows executable) and `ofscraper_windows_3_16_1.zip` (Windows zip)
* `ofscraper_linux_3_16_1` and `ofscraper_linux_3_16_1.zip` (Linux)
* `ofscraper_macos_3_16_1` and `ofscraper_macos_3_16_1.zip` (macOS)
