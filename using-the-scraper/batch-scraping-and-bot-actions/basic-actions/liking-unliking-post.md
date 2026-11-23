# Liking/Unliking Post

***

## Liking/Unliking content

```sh
ofscraper --action like
```

```sh
ofscraper --action unlike
```

***

## Selecting Posts

### By post type

Pass a comma-separated list of post areas to target:

```sh
ofscraper --action like --posts pinned,timeline
```

Or repeat `--posts`:

```sh
ofscraper --action like --posts pinned --posts timeline
```

### Options

* `timeline`
* `archived`
* `pinned`
* `streams`
* `labels`

#### Special Options

* `all`: scrapes `timeline`, `archived`, `pinned`, and `streams`
* `labels*` or `labels+`: scrapes `all` plus `labels`

#### remove post type

Exclude a post type by prepending a hyphen (`-`), such as `-pinned`. This overrides any other selection, including `all`. Hyphen exclusions only work with `--posts`, not with `--like-area` or `--download-area`.

## Limits

### Onlyfans rate limit

Estimated to be around 1,000 per day.

### Limit in program

* Each like/unlike request has a delay to avoid spamming the OnlyFans server and causing logouts.
* The delay is randomised between `0.9` and `3.5` seconds by default.
* If a like or unlike fails, the post is marked as failed.
