# Example Configs

A new `config.json` is written from the built-in defaults. Environment variables apply at runtime only and aren't saved into it.

## Example 1

```json
{
    "config": {
        "main_profile": "main_profile",
        "metadata": "{configpath}/{profile}/.data/{model_username}_{model_id}",
        "discord": "",
        "file_options": {
            "save_location": "~/Data/ofscraper",
            "dir_format": "{model_username}/{responsetype}/{mediatype}/",
            "file_format": "{filename}.{ext}",
            "textlength": 0,
            "space_replacer": " ",
            "date": "MM-DD-YYYY",
            "text_type_default": "letter",
            "truncation_default": true
        },
        "download_options": {
            "filter": [
                "Images",
                "Audios",
                "Videos"
            ],
            "auto_resume": true,
            "system_free_min": 0
        },
        "binary_options": {
            "ffmpeg": "~/.config/ofscraper/bin/ffmpeg"
        },
        "cdm_options": {
            "private-key": "~/.config/ofscraper/device/private_key.pem",
            "client-id": "~/.config/ofscraper/device/client_id.bin",
            "key-mode-default": "manual"
        },
        "performance_options": {
            "download_sems": 10
        },
        "content_filter_options": {
            "file_size_max": 0,
            "file_size_min": 0
        },
        "advanced_options": {
            "dynamic-mode-default": "dc",
            "downloadbars": false,
            "cache-mode": "sqlite",
            "sanitize_text": false,
            "temp_dir": null
        },
        "responsetype": {
            "timeline": "Posts",
            "message": "Messages",
            "archived": "Archived",
            "paid": "Messages",
            "stories": "Stories",
            "highlights": "Stories",
            "profile": "Profile",
            "pinned": "Posts"
        }
    }
}
```

## Digitalcriminals Example

```json
{
    "config": {
        "main_profile": "main_profile",
        "metadata": "{save_location}/{model_username}/Metadata",
        "discord": "",
        "file_options": {
            "save_location": "~/Data/ofscraper",
            "dir_format": "{model_username}/{responsetype}/{value}/{mediatype}/",
            "file_format": "{filename}.{ext}",
            "textlength": 0,
            "space_replacer": " ",
            "date": "MM-DD-YYYY",
            "text_type_default": "letter",
            "truncation_default": true
        },
        "download_options": {
            "filter": [
                "Images",
                "Audios",
                "Videos"
            ],
            "auto_resume": true,
            "system_free_min": 0
        },
        "binary_options": {
            "ffmpeg": "~/.config/ofscraper/bin/ffmpeg"
        },
        "cdm_options": {
            "private-key": "~/.config/ofscraper/device/private_key.pem",
            "client-id": "~/.config/ofscraper/device/client_id.bin",
            "key-mode-default": "manual"
        },
        "performance_options": {
            "download_sems": 10
        },
        "content_filter_options": {
            "file_size_max": 0,
            "file_size_min": 0
        },
        "advanced_options": {
            "dynamic-mode-default": "dc",
            "logs_expire_time": 0,
            "downloadbars": false,
            "cache-mode": "sqlite",
            "sanitize_text": false,
            "temp_dir": null
        },
        "script_options": {
            "after_download_script": null,
            "post_script": null
        },
        "responsetype": {
            "timeline": "Posts",
            "message": "Messages",
            "archived": "Archived",
            "paid": "Messages",
            "stories": "Stories",
            "highlights": "Stories",
            "profile": "Profile",
            "pinned": "Posts"
        }
    }
}
```
