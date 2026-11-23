# Responsetype Placeholders

Use `responsetype` in `config.json` to group downloads into folders by content type. You can merge multiple response types into one folder (for example, `stories` and `highlights` together, or `paid` and `message` into `Premium`), or keep each type in its own folder (for example, `timeline` in `Posts`).

The valid keys are `timeline` (`post` also works), `message` (for message posts), `archived`, `paid`, `stories`, `highlights`, `profile`, `pinned`, and `streams`. In each key-value pair, leave the left-hand key unchanged and set the right-hand value to the folder name you want `{responsetype}` to produce. The scraper capitalises only the first letter and lower-cases the rest, so `MyPremium` becomes `Mypremium`.

## Default folders

| Response type | Default folder |
|---|---|
| `timeline` | `Posts` |
| `message` | `Messages` |
| `archived` | `Archived` |
| `paid` | `Messages` |
| `stories` | `Stories` |
| `highlights` | `Stories` |
| `profile` | `Profile` |
| `pinned` | `Posts` |
| `streams` | `Streams` |

#### Example

```json
"timeline": "posts",
"message": "premium",
"archived": "archived",
"paid": "premium",
"stories": "stories",
"highlights": "stories",
"profile": "profile",
"pinned": "posts",
"streams": "streams"
```

With `"dir_format": "{model_username}/{responsetype}/{mediatype}/"`:

| Response type | Mapped value | Saved path |
|---|---|---|
| `timeline` | `posts` | `{model_username}/Posts/{mediatype}/` |
| `message` | `premium` | `{model_username}/Premium/{mediatype}/` |
| `archived` | `archived` | `{model_username}/Archived/{mediatype}/` |
| `paid` | `premium` | `{model_username}/Premium/{mediatype}/` |
| `stories` | `stories` | `{model_username}/Stories/{mediatype}/` |
| `highlights` | `stories` | `{model_username}/Stories/{mediatype}/` |
| `profile` | `profile` | `{model_username}/Profile/{mediatype}/` |
| `pinned` | `posts` | `{model_username}/Posts/{mediatype}/` |
| `streams` | `streams` | `{model_username}/Streams/{mediatype}/` |
