# Install from source

This guide explains how to install and set up OF-Scraper from source.

> ℹ️ **Note for developers:** Development builds get a version with the commit hash added (for example `3.16.2+g1a2b3c4`). PyPI doesn't accept versions like that, so only tagged releases are published there as `ofscraper-community`. The version comes from your Git tags: the build's version script (`plugins.py`, run through `version-pioneer`) takes the newest version tag and adds the commit hash. Pulling tags in step 2 makes sure local builds get the right version.

## Prerequisites

Make sure you have both of these installed:

* **Git:** for cloning the repository. See the [Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
* **uv:** a fast Python package installer and resolver. See the [uv installation guide](https://docs.astral.sh/uv/getting-started/installation/).

## Installation Steps

### 1. Clone the Repository

```sh
git clone https://github.com/cloakedkeys/OF-Scraper-Community
cd OF-Scraper-Community
```

### 2. Pull the Latest Tags

Pull Git tags so the build can work out the version from them:

```sh
git pull --tags
```

### 3. Create a Python Virtual Environment

Using a virtual environment is **highly recommended** to isolate the project's dependencies from your system Python. Create a `.venv` directory in the project folder (Python 3.11 to 3.15 are supported):

```bash
uv venv
```

### 4. Activate the Virtual Environment

On Linux or macOS:

```bash
source .venv/bin/activate
```

On Windows (PowerShell):

```powershell
.\.venv\Scripts\activate
```

Your terminal prompt should now show a prefix such as `(.venv)` or `OF-Scraper`.

### 5. Install Project Dependencies

Install dependencies from `pyproject.toml` and `uv.lock` into the active virtual environment:

```bash
uv sync --reinstall
```

`--reinstall` reinstalls packages that are already present, which is useful after pulling updates.
