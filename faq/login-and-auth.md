# Login & Auth

## Trouble logging in

* Check the formatting of `auth.json` (see [Auth](../getting-started/auth.md)).
* Use `--auth-fail` to make a run quit on an auth error instead of prompting again.
* Try changing `dynamic-mode-default` (see [Advanced config options](../getting-started/config-options/options/advanced-config-options.md)).

***

## "Double check auth info"

* Copy every value (`sess`, `auth_id`, `x-bc`, `user_agent`) again from the same browser while you're logged in to OnlyFans. They expire when you log out.
* `user_agent` must match that browser exactly.
* Make sure you're on the latest version of this fork.

***

## "No accounts found during scan"

Usually an auth problem, so check the answer above first. Then check you have an active subscription to the creator, and that you aren't filtering it out with options like `--expired-subscription`.

***

## Status Down

This usually means your authentication details are wrong, or you've been signed out of OnlyFans.

***

## Downloads fail with 403 after a reconnect or VPN switch

OnlyFans download links are signed for the IP that fetched them. From 3.16.11, a link rejected with a 403 is fetched again and the download resumes from its `.part` file; 3.16.12 extends this to stories, highlights, and DRM video. Update if every remaining download fails after your IP changes.
