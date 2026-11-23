---
description: Getting OF-Scraper onto your system
---

# Install

***

## Version Info

> ℹ️ **This fork is on PyPI as `ofscraper-community`.** The command is still `ofscraper`. `datawhores/OF-Scraper` also publishes this same code as `ofscraper` (versions `3.14.7` and older are upstream's old code without the fork's fixes).

> ℹ️ Check the [GitHub Releases page](https://github.com/cloakedkeys/OF-Scraper-Community/releases) for the latest release.

[![drawing](https://img.shields.io/github/v/release/cloakedkeys/OF-Scraper-Community?label=release&color=00a8e8)](https://github.com/cloakedkeys/OF-Scraper-Community/releases/latest)

***

## Before Starting

This guide assumes you have your terminal open and Python installed. If you need help with that first, see:

[Installing Prerequisites](pre-install-guide/)

***

## Install via a package manager

> ℹ️ **uv is recommended.** It installs each tool in its own isolated virtual environment, which:
>
> * **Prevents conflicts** with other Python packages or system-wide installs.
> * **Simplifies updates** when new releases come out.

### **Option 1: uv Install**

[UV Install](uv-install.md)

### **Option 2: pipx install**

```sh
pipx install ofscraper-community
```

Like `uv`, `pipx` gives the tool its own environment.

### **Option 3: PIP install**

```sh
pip install ofscraper-community
```

Use a virtual environment, as `pip` installs into the current Python environment.

To use [PostgreSQL](../page/postgresql.md) instead of a database file per creator, install the `postgres` extra:

```sh
pip install "ofscraper-community[postgres]"
```

The extra needs 3.18.0 or later. See the [PostgreSQL page](../page/postgresql.md#what-you-need).

> ℹ️ **Don't install `ofscraper` and `ofscraper-community` together with pip.** Both provide the `ofscraper` command, so they overwrite each other. Run `pip uninstall ofscraper` first. If you already have both, uninstall both and then install `ofscraper-community` again. `uv` and `pipx` keep each tool separate, so they don't have this problem.

To get the latest changes on `main` before they're released, install from GitHub:

```sh
pip install git+https://github.com/cloakedkeys/OF-Scraper-Community
```

## Install via Docker

[Docker](docker.md)

## Compiled Binaries \[No Install]

> ℹ️ A PyInstaller binary bundles OF-Scraper, Python, and its dependencies into a single executable or folder, so you can run it without installing Python.

> ℹ️ Support for issues specific to PyInstaller may be limited.

[Binary Releases](binary-releases.md)
