# Migrating from Digitalcriminal's script

***

## Set Metadata

> ℹ️ Your previous metadata files are compatible, so only the path needs to match.

[Setting metadata path](config-options/setting-metadata-path.md)

***

## Set save path

> ℹ️ Most settings are transferable, including the defaults.

[File Output Options](config-options/file-output-options/)

## Example

See the Digitalcriminals example in [Example Configs](config-options/example-configs.md).

### save\_location

```text
"save_location": "/Onlyfans",
```

### dir format

```text
"dir_format": "{model_username}/{responsetype}/{value}/{mediatype}/"
```

Together, these produce a full path like:

```text
/Onlyfans/modelA/Messages/Free/Images/
```

1. `/Onlyfans` comes from `save_location`.
2. `modelA/Messages/Free/Images/` comes from `dir_format`.

### metadata

```text
"metadata": "{save_location}/{model_username}/Metadata"
```

Here `{save_location}` is the save location from `config.json`. This sets the directory where `user_data.db` is stored, for example:

```text
/Onlyfans/ModelA/Metadata
```
