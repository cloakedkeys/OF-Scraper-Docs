---
description: Options required for protected downloads
---

# CDM Options

## key-mode-default

The default Content Decryption Module (CDM) used for decrypting content. Default: `manual`.

* `manual`: uses the local CDM files from `private-key` and `client-id`.
* Other values fall back to the default.

> ⚠️ **Deprecated:** `cdrm` is deprecated: the service no longer works and the option will be removed. It also sends your request headers, cookies included, to `cdrm-project.com`.

Certain CDMs might need additional configuration. See [CDM Setup](../../cdm-options/).

You can override this setting on the command line with `--key-mode` (or `-k`).

***

## private-key

Path to the CDM private key file (`private_key.pem`), used for `manual` CDM.

> ℹ️ **Fork:** A path with surrounding quotes, as Windows' "Copy as path" produces, is accepted. The same applies to `client-id`, `ffmpeg`, and `temp_dir`.

## client-id

Path to the CDM client ID file (`client_id.bin`), used for `manual` CDM.
