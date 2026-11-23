# UV Install

## Installing UV

> ⚠️ **Important:** UV is a standalone binary, so you don't need Python installed on your system first. Once UV is installed, it can install and manage Python versions for you. Installing UV with one of its official installation scripts is recommended for the most straightforward setup.

[pre-install-guide](pre-install-guide/ "mention")

## Installing/Upgrading OF-Scraper

> ℹ️ **Tip:** Add `--verbose` to see more details about the install process.

### **Stable Release Install**

Install the latest release of this fork from PyPI. The package is `ofscraper-community`; the command is still `ofscraper`. (`datawhores/OF-Scraper` also publishes this same code as `ofscraper`; versions `3.14.7` and older are upstream's old code without the fork's fixes.)

```bash
uv tool install ofscraper-community
```

### Development Release

Install the latest code on `main` from GitHub before it's released. To install a specific branch, add `@<branch>`:

```bash
uv tool install git+https://github.com/cloakedkeys/OF-Scraper-Community --force
```

### Specific Version of Script

To install a specific release, add `==<version>`:

```bash
uv tool install ofscraper-community==3.16.2 --force
```

Releases older than 3.16.2 aren't on PyPI. Install those from GitHub by tag (tags are listed on the [releases page](https://github.com/cloakedkeys/OF-Scraper-Community/releases)):

```bash
uv tool install git+https://github.com/cloakedkeys/OF-Scraper-Community@3.16.1 --force
```

### Specific Version of Python

Specify which Python version `uv` should use by adding `--python <version>`:

```bash
# Example: install with Python 3.12 (3.11 to 3.15 are supported)
uv tool install ofscraper-community --python 3.12 --force
```

### Including pyffmpeg (Optional)

`pyffmpeg` is a Python package that bundles its own `ffmpeg` binaries. Add `[ffmpeg]` to the package name to include it:

```bash
uv tool install "ofscraper-community[ffmpeg]" --force
```

> ℹ️ Installing `ofscraper-community[ffmpeg]` pulls in `pyffmpeg` as a dependency. `pyffmpeg` manages its own `ffmpeg` binary, so you generally don't need to install `ffmpeg` separately.

### Upgrade

```bash
uv tool upgrade ofscraper-community
```

If you installed from GitHub, run the same install command again.

> ℹ️ **Installed the fork before it was on PyPI?** That install is called `ofscraper` in `uv`. Remove it first, then install from PyPI:
>
> ```bash
> uv tool uninstall ofscraper
> uv tool install ofscraper-community
> ```
