# Content Check Modes

## What is this

<figure><img src="../.gitbook/assets/image2.png" alt=""><figcaption></figcaption></figure>

Content check mode scrapes data from OnlyFans.com and displays it in a searchable, filterable table. The check table is for OnlyFans only.

Each media item gets its own row with details including:

* Price of the content
* Whether the media is in your library (based on media ID)
* Whether the media is unlocked (a missing value shows as locked)
* The post the media belongs to
* Date the media was posted
* Text included with the media
* Length of the media

Check modes use caching to speed up runs. The cache is built during regular scraping or content check runs and lasts 3 days before refreshing. Pass `--force` to fetch fresh data immediately.

***

## Opening it from the menu

Run `ofscraper`, choose **Perform Action(s)**, then **Browse and pick media (check table)**. Pick the creators as usual, then the table: **Posts**, **Messages**, **Paid**, or **Stories**.

* While the media is fetched, the same page progress as a normal scrape is shown.
* When you close the table, any downloads you sent from it finish, then you're back at the menu.
* The menu uses the commands' defaults: a creator's saved post list when there is one, and for Posts the Timeline, Pinned, Archived, and Streams areas. To fetch a fresh list or pick other areas, use the commands below with `--force` or `--check-area`.
* Settings the table changes don't carry over to the next run.

See [Table Management](table-management/README.md) for picking and downloading media in the table.

***

## cmdline arguments

### Post Check Mode

Review posts on the main timeline, or paid content accessed through a post URL:

* Pass `--url` or `--file` (areas come from `--check-area`, default Timeline, Pinned, Archived, and Streams). You can combine both options.
* `--url` splits on commas and spaces, and can be passed more than once.
* `--file` can also be passed more than once, and every file is read; lines inside a file aren't split on commas.

#### Examples

```sh
ofscraper post_check --url url1,url2,url3
ofscraper post_check --url url1 --url url2
ofscraper post_check --file file
ofscraper post_check --file file --url url
```

#### File

Put one accepted URL per line.

#### Accepted urls

| Type | Example |
|---|---|
| Post page | `https://onlyfans.com/1113331313/creator` |
| Creator page | `https://onlyfans.com/creator` |
| Creator name | `creator` |
| Creator ID | `11131313` |

### Message Check Mode

Works like `post_check`, differing only in the accepted URL types. When the cache expires, all messages must be scraped again.

#### Examples

All of the `post_check` patterns work here too:

```sh
ofscraper msg_check --url url1,url2,url3
```

#### Accepted urls

| Type | Example |
|---|---|
| Chat page | `https://onlyfans.com/my/chats/chat/11131313/` |
| Creator name | `creator` |
| Creator ID | `11131313` |

### Paid Check Mode

Gathers paid content for the specified creators:

* Pass `--username` or `--file` (you can combine both).
* `--username` splits on commas and spaces, and can be passed more than once.
* `--file` can also be passed more than once, and every file is read; lines inside a file aren't split on commas.

#### Examples

```sh
ofscraper paid_check --username username1,username2
ofscraper paid_check --username username1 --username username2
ofscraper paid_check --file file
ofscraper paid_check --file file --username username
```

#### File

Put one username per line.

#### Accepted username

| Type | Example |
|---|---|
| Creator name | `creator` |
| Creator ID | `11131313` |

### Story Check Mode

Collects stories and highlights for the specified creators.

> ℹ️ Stories are temporary content and may change frequently.

* Pass `--username` or `--file` (you can combine both).
* `--username` splits on commas and spaces, and can be passed more than once.
* `--file` can also be passed more than once, and every file is read; lines inside a file aren't split on commas.

#### Examples

```sh
ofscraper story_check --username username1,username2
ofscraper story_check --username username1 --username username2
ofscraper story_check --file file
ofscraper story_check --file file --username username
```

#### File

Put one username per line.

### Getting latest content

In each mode, creator data is cached (3 days for `msg_check`). Add `--force` to fetch the latest content:

```sh
ofscraper msg_check --url url --force
```
