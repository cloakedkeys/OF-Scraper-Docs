# HTTP Errors & Fansly

## 404 Response

The content is no longer available, or the creator has deleted their account.

***

## 409 Response

Content is unavailable on the OnlyFans site itself (shown as placeholders or media that won't load).

VPN users often see this depending on which VPN server they're connected to; it also affects the API, so OF-Scraper can't scrape that content either. Switch VPN servers, or wait a while for it to reset.

***

## 429 Response

* Usually caused by too many requests, especially when auto-liking or unliking.
* The limit appears to be around 1,000 per day.

***

## Request taking a long time

When a request fails, OF-Scraper pauses and retries several times. Frequent retries can make runs take longer.

> ℹ️ Requests have a built-in time limit so they don't hang forever (the read timeout is 60 seconds by default). You can override that default by setting the `OFSC_READ_TIMEOUT` environment variable.

***

## Something is not working

Display debug output in the console:

```sh
ofscraper --output debug
```

Or write debug logs to your configuration folder:

```sh
ofscraper --log debug
```

Attach the log to a GitHub issue (or share it in Discord).

***

## Fansly login or download problems

See [Fansly](../fansly.md) for how to get the token and user agent.
