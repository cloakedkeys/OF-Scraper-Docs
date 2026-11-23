# Basic Actions

The things a command-line run can do, one page each.

* [Liking/Unliking Post](liking-unliking-post.md)
* [Downloading Content](selecting-posts/README.md)

## Multiple Actions

> ℹ️ `--posts` is shorthand for selecting both `--like-area` and `--download-area`.

> ℹ️ `--like-area` and `--download-area` take precedence over `--posts`.

```sh
ofscraper --action like,download --like-area pinned --download-area timeline
```
