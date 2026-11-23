# Docker

## Volumes

> ⚠️ **If you manually download binaries, mount the Linux binaries from your host system into the container.** See the [Docker Compose](#docker-compose) section for an example.

| Mount Point | Purpose | Typical Default Location |
|---|---|---|
| **APP\_HOME** | The **home directory** for the application's user inside the container. Often used as the base for other default paths. | `/home/ofscraper` |
| **DATA\_DIR** | Where the application stores **persistent data**, such as databases, downloaded content, and media. Sets the default save path. | `$APP_HOME/data` (e.g. `/home/ofscraper/data`) |
| **CONFIG\_DIR** | Which folder the start script creates and gives the container user ownership of. | `$APP_HOME/.config` (e.g. `/home/ofscraper/.config`) |

### CONFIG\_DIR

`CONFIG_DIR` only sets which folder the start script creates and gives the container user ownership of. The app doesn't read `CONFIG_DIR`: config comes from `~/.config/ofscraper` or `--config`, so setting `CONFIG_DIR` doesn't move the config.

| Scenario | `CONFIG_DIR` Environment Variable | `APP_HOME` Value (Example) | `CONFIG_DIR` Final Path | Explanation |
|---|---|---|---|---|
| **1. Explicitly Set** | `CONFIG_DIR=/app/config/` | `/home/ofscraper` | `/app/config` | The start script creates and owns `/app/config`, but the app still reads config from `~/.config/ofscraper` or `--config`. |
| **2. Not Set / Empty** | Unset or `CONFIG_DIR=""` | `/home/ofscraper` | `/home/ofscraper/.config` | Defaults to `.config` inside `APP_HOME`. |

### DATA\_DIR

`DATA_DIR` sets the default save path for persistent data and respects explicit overrides.

| Scenario | `DATA_DIR` Environment Variable | `APP_HOME` Value (Example) | `DATA_DIR` Final Path | Explanation |
|---|---|---|---|---|
| **1. Explicitly Set** | `DATA_DIR=/app/data` | `/home/ofscraper` | `/app/data` | Uses the value you set directly, overriding the default. |
| **2. Not Set / Empty** | Unset or `DATA_DIR=""` | `/home/ofscraper` | `/home/ofscraper/data` | Defaults to `data` inside `APP_HOME`. |

### Home Folder

The container's home directory is controlled by `APP_HOME`, a full path that defaults to `/home/ofscraper`. It doesn't change when the username changes.

***

## Environment Variables

The container is managed by an entrypoint script that creates a non-root user to run the application. You can control the user, group, paths, and script behaviour with the environment variables below.

### Fork changes

> ℹ️ **Since 3.15.0.** These apply to images from 3.15.0 on. See [Fork Changes](../fork-changes.md).

* **Downloads go to the mounted data folder by default.** With no `save_location` in your config, downloads are saved to `DATA_DIR` (`/home/ofscraper/data`), the folder `docker-compose.yml` mounts. Upstream saved them to `/home/ofscraper/Data/ofscraper`, which isn't mounted. A `save_location` in your config, a custom `DATA_DIR` or `OFSC_SAVE_PATH_DEFAULT` still take priority.
* **Both sets of user variables work.** `USER_ID`, `GROUP_ID`, `USER_NAME` and `GROUP_NAME` (the names in `docker-compose.yml`) are read as well as `UID`, `GID`, `USERNAME` and `GROUPNAME`. The first set takes precedence. A lone user ID is also used for the group, and a lone group ID keeps the default user ID 1000.
* **Non-root containers start.** With `docker run --user 1234:1234` or compose `user:`, the entrypoint skips user creation and `chown`, and runs as that user. Mounted folders must already be writable by it.
* **ffmpeg works on arm64.** Every image includes ffmpeg: amd64 uses `pyffmpeg`'s ffmpeg, and arm64 uses a static ffmpeg 9.0.2.
* **`docker stop` works in daemon mode.** SIGTERM stops the scraper promptly instead of waiting for Docker to kill it, including while it's waiting between passes.
* **Start the next daemon pass early** with `docker kill --signal=SIGUSR1 <container>`. See [`--daemon`](../command-reference/shared-options/scrape-metadata-options/general-scraper-args.md).

### User and Group Identity

These variables control the user that runs the application inside the container. The start script reads `USER_ID`, `GROUP_ID`, `USER_NAME`, and `GROUP_NAME` first, then falls back to `UID`, `GID`, `USERNAME`, and `GROUPNAME`.

For mounted volumes, setting the user and group IDs to match your host user (e.g. `-e USER_ID=$(id -u) -e GROUP_ID=$(id -g)`) is **highly recommended**.

| Environment Variable | Default | Purpose |
|---|---|---|
| `USER_ID` / `UID` | `1000` | Sets the **numeric User ID (UID)** so files created on mounted volumes are owned by your host user. If this UID already belongs to another user in the container, the script adapts and uses that user. |
| `GROUP_ID` / `GID` | `1000` | Sets the **numeric Group ID (GID)** for the user's primary group. Like `USER_ID` / `UID`, the script adapts if this GID already belongs to an existing group. |
| `USER_NAME` / `USERNAME` | `ofscraper` | Sets the **username** created inside the container. If the UID already belongs to a different user, the script uses that existing username instead and logs a message. |
| `GROUP_NAME` / `GROUPNAME` | Value of `USER_NAME` / `USERNAME` | Sets the **primary group name**. Secondary to the GID, like the username is to the UID. |

### Path and Directory Management

These variables control the container's paths.

| Environment Variable | Default | Purpose |
|---|---|---|
| `APP_HOME` | `/home/ofscraper` | Full path for the application user's home directory inside the container. Doesn't change with the username. |
| `DATA_DIR` | `$APP_HOME/data` | Sets the data folder and, unless `OFSC_SAVE_PATH_DEFAULT` is set, the default save path. Set to any absolute path (such as `/data`) if you prefer to mount a volume there. |
| `CONFIG_DIR` | `$APP_HOME/.config` | Sets which folder the start script creates and gives the container user ownership of. Doesn't change where the app reads config (`~/.config/ofscraper` or `--config`). |

### Script Behavior Flags

| Environment Variable | Default | Purpose |
|---|---|---|
| `KEEP_PERM` | `false` | When `true`, skips running `chown` on the home, data, and config directories. Useful for rootless Docker or when managing host permissions manually. |

***

## Docker Run

Replace `/your/host/config/path/` with your host config folder, `/your/host/data/path/` with your host downloads folder, and `{args}` with your OF-Scraper arguments (for example, `--username myonlyfans`).

### Minimal `docker run` Command

Uses the container's default user and group (`ofscraper`, UID/GID `1000`):

```bash
docker run -it --rm --name=ofscraper \
  -v /your/host/config/path/:/home/ofscraper/.config/ofscraper/ \
  -v /your/host/data/path/:/home/ofscraper/data \
  ghcr.io/cloakedkeys/of-scraper-community:latest ofscraper {args}
```

#### Using Optional Environment Variables

Pass optional variables with `-e` (`GROUP_NAME` is only needed if you want a group name different from `USER_NAME`):

```bash
docker run -it --rm --name=ofscraper \
  -v /your/host/config/path/:/home/ofscraper/.config/ofscraper/ \
  -v /your/host/data/path/:/home/ofscraper/data \
  -e USER_NAME=youruser \
  -e USER_ID=$(id -u) \
  -e GROUP_ID=$(id -g) \
  -e GROUP_NAME=yourgroup \
  ghcr.io/cloakedkeys/of-scraper-community:latest ofscraper {args}
```

***

## Docker Compose

For persistent setups, use Docker Compose. If you choose to mount `ffmpeg` from the host, install `ffmpeg` on your host system first.

```yaml
services:
  of-scraper:
    stdin_open: true # Keeps STDIN open for interactive processes
    tty: true # Allocates a pseudo-TTY for a terminal-like interface
    container_name: ofscraper
    
    environment: # Optional environment variables
      # These are recommended for correct file permissions on mounted volumes.
      # Default UID/GID is 1000:1000 if not specified via environment variables in your shell.
      # - USER_NAME=ofscraper   # Defaults to 'ofscraper' in the entrypoint script
      # - USER_ID=${USER_ID}   # Host user's UID (e.g., set via 'export USER_ID=$(id -u)' on host)
      # - GROUP_ID=${GROUP_ID} # Host user's GID (e.g., set via 'export GROUP_ID=$(id -g)' on host)
      # - GROUP_NAME=mygroup # Optional: If you want a custom group name different from USER_NAME
    volumes:
      # Mount your configuration directory (replace ./config/ with your host path)
      - ./config/:/home/ofscraper/.config/ofscraper/
      # Mount your data storage directory (replace ./data/ with your host path)
      - ./data/:/home/ofscraper/data/
      # Optional: Mount pre-installed binaries from host (adjust paths as needed)
      # - /usr/bin/ffmpeg:/usr/bin/ffmpeg

    image: ghcr.io/cloakedkeys/of-scraper-community:latest 
    # --- COMMAND OPTIONS ---
    # Choose one of the following 'command' configurations based on your use case.
    # Uncomment the desired option and ensure others are commented out.

    # Option 1: For interactive use (recommended if you frequently run commands manually)
    # This keeps the container running indefinitely in the background.
    command: ["/bin/bash", "-c", "sleep infinity"]
    # To bring the container up: `docker compose up -d`
    # Then, to run commands inside it: `docker compose exec -it ofscraper ofscraper {args}`
    # Example: `docker compose exec -it ofscraper ofscraper --username myuser`

    # Option 2: To run the scraper automatically with specific arguments when the container starts
    # Uncomment the line below and comment out Option 1 above.
    # command: "ofscraper --username ALL --posts all"

    # Optional: Configure restart policy.
    # restart: "unless-stopped" # Ensures the container restarts automatically unless explicitly stopped.
```

***

### Interactive Use

If your `docker-compose.yml` uses `command: ["/bin/bash", "-c", "sleep infinity"]`, start the container in detached mode with `docker compose up -d`, then run commands inside it:

```bash
docker compose exec -it ofscraper ofscraper {args}
```

Replace `{args}` with your OF-Scraper arguments, for example:

```bash
docker compose exec -it ofscraper ofscraper --username myuser --posts all
```

***

## Building Custom Images

> ℹ️ **Every image includes `ffmpeg` with no build argument:** `amd64` uses `pyffmpeg`'s `ffmpeg`, and `arm64` uses a static `ffmpeg 9.0.2`. You generally don't need to install `ffmpeg` on your host system or mount it into the container.

This section is only needed if you're building the Docker image locally from source (for example, to customise the build or add Python dependencies).

### Build Arguments

The only build argument is `BUILD_VERSION`, which is optional (otherwise the version is taken from git).

```bash
# Optional: Create a builder instance for multi-platform builds (recommended for cross-platform compatibility)
# docker buildx create --name mybuilder --use

# Navigate to the directory containing your Dockerfile
# cd /path/to/OF-Scraper/repository

# Build for one platform and load into local Docker
docker buildx build --platform linux/amd64 -t my-ofscraper-image:latest --load .
```

A two-platform build (`--platform linux/amd64,linux/arm64`) needs `--push` instead of `--load`.

***

## Releases

Images are published on [GitHub Container Registry (ghcr.io)](https://github.com/cloakedkeys/OF-Scraper-Community/pkgs/container/of-scraper-community).

***

## Tags

The fork publishes only these image tags on GHCR:

| Syntax | Example | What it is |
|---|---|---|
| `latest` | `latest` | The newest `main` build |
| `main` | `main` | The newest `main` build |
| `<version>-<hash>-<timestamp>` and `<version>-<hash>` | `3.17.1-9e54ed3-1749940070` | Snapshot build for a commit |
| `X.Y.Z` | `3.17.1` | Release build |
