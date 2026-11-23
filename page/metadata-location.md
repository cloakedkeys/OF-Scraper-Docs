# Metadata location

Each creator has one `user_data.db` in the folder set by the `metadata` config value. The default is `{configpath}/{profile}/.data/{model_id}`, for example `~/.config/ofscraper/main_profile/.data/<model_id>/user_data.db`.

Backups are kept in a `backup` folder beside the database.

Fansly runs use a separate `Fansly` subfolder when the template has no site-specific field, so Fansly rows do not land in the OnlyFans file.
