# CDM Setup

To handle encrypted content, you need a CDM (Content Decryption Module). You'll know it's needed if you see `tempvideo` and `tempaudio` files. Decrypting also requires `ffmpeg` 6 or newer.

### Manual

This method is recommended for its reliability and independence from third-party service outages or shutdowns.

#### Setup

1. Follow the [KeyDive README](https://github.com/hyugogirubato/KeyDive/blob/main/README.md) to extract your two CDM files:
   * Private key file (`private_key.pem`)
   * Client ID file (`client_id.bin`)
2. Save both files to an easily accessible location.

> ℹ️ **The default key mode is `manual`.** You only need to set the two file paths below.

#### Changing via config manually

In the `cdm_options` section of `config.json`, if your config still says `cdrm`, change `key-mode-default` to `manual`:

```text
"key-mode-default": "manual"
```

Set `private-key` and `client-id` to the full paths of your CDM files (quotes from Windows' "Copy as path" are accepted):

```text
"private-key": ".../private_key.pem"
"client-id": ".../client_id.bin"
```

You can also pass `--key-mode manual`, `--private-key`, and `--client-id` for a single run.

#### Changing via the prompt menu

1. From the main menu, go to **Edit config.json file** → **CDM Options**.

<details>

<summary>prompt menu</summary>

[Using Prompts](../using-the-scraper/using-prompts/README.md)

</details>

2. When prompted, choose `manual` for the key mode, then enter the full path for `client-id` and `private-key` (in that order).

### CDRM

> ⚠️ **Deprecated:** `cdrm` is deprecated and will be removed. The default address (`cdrm-project.com`) is never contacted, so protected videos fail in `cdrm` mode with a message to use `manual`. It works only with a server you run yourself (set in `OFSC_CDRM_URL`), and that server receives your request headers and cookies.

#### Changing via config manually

Set `key-mode-default` in `config.json`:

```text
"key-mode-default": "cdrm"
```

Or pass `--key-mode` on the command line:

```sh
--key-mode cdrm
```

#### Changing via the prompt menu

1. From the main menu, go to **Edit config.json file** → **CDM Options**.
2. Choose `cdrm` when prompted for the key mode.
