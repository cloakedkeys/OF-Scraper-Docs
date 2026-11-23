---
description: Copy what OF-Scraper knows about your downloads into Stash
---

# Organize Downloads in Stash

[Stash](https://stashapp.cc) is a self-hosted media library. It indexes your download folders, but on its own it only knows file names. `stash_sync` copies what OF-Scraper recorded about each file into Stash, for OnlyFans and Fansly downloads.

> ℹ️ **Since 3.16.6.** See [Fork Changes](../../fork-changes.md).

***

## What it fills in

| Field | OnlyFans | Fansly |
|---|---|---|
| **Performers** | The creator, with a link to their OnlyFans page | The creator, with a link to their Fansly page, and anyone @mentioned in the caption |
| **Studio** | `OnlyFans` | `Fansly` |
| **Date** | When the post or message was posted | Same |
| **Title and details** | The caption's first line, and the full caption | Same |
| **Code** | The post ID (none for profile pictures) | The Fansly media ID |
| **URL** | The post's page, for timeline posts and bought posts | `https://fansly.com/post/<id>` for timeline posts, and `https://fansly.com/messages/<conversation>` for messages |
| **Tags** | Where the file came from, e.g. `OnlyFans Timeline`, `OnlyFans Messages`, or `OnlyFans Paid` | Same with `Fansly`, plus `Fansly Preview` for preview media and the caption's #hashtags, lowercased |
| **Gallery** | None | One per post or message, holding its images and scenes |

* It only fills in empty fields and adds performers, the studio, tags, and galleries. Anything you've set in Stash is kept, so running it again changes nothing that's already there.
* It reads OF-Scraper's databases offline and never contacts OnlyFans or Fansly.
* OnlyFans messages get no URL, since a message has no public page. Fansly purchases aren't posts, so their files get no gallery.
* Databases from older versions may lack a Fansly message's conversation ID or an OnlyFans purchase's type. Such files get no URL until a messages or purchases scan fills it in; the next sync then adds the link.

***

## Run it

1. Make sure Stash is running and has already scanned your download folders (or add `--scan` when running with `--apply` below).
2. Preview what would change:

   ```sh
   python -m ofscraper.commands.stash_sync "<profile>/.data"
   ```

3. Apply the changes:

   ```sh
   python -m ofscraper.commands.stash_sync "<profile>/.data" --apply
   ```

`<profile>/.data` holds one folder per creator, each with a `user_data.db`. To sync a single creator, pass that creator's `user_data.db` instead. Fansly runs keep their databases in a `Fansly` folder under `.data` by default.

The report is JSON. For each creator it counts:

| Count | Meaning |
|---|---|
| `to_update` / `updated` | Files that would be, or were, changed in Stash |
| `up_to_date` | Files that already had everything |
| `not_in_stash` | Downloaded files Stash hasn't indexed; scan, or check `--path-map` |
| `unsupported_type` | Audio, which Stash doesn't index |
| `galleries_to_create` / `galleries_created`, `galleries_to_update` / `galleries_updated`, `galleries_up_to_date` | Fansly galleries, counted the same way |

A few of the missing paths are listed under `not_in_stash_sample`.

***

## Options

| Option | Use |
|---|---|
| `--apply` | Write to Stash; without it, nothing is created or changed |
| `--postgres` | *(In releases after 3.17.1.)* Read the PostgreSQL database `$OFSC_DATABASE_URL` names instead of `user_data.db` files; give no paths with it |
| `--site`, `--creator` | With `--postgres`: sync one site (`onlyfans` or `fansly`), or only creators matching an ID or username (repeatable) |
| `--scan` | With `--apply`, have Stash scan the download folders first and wait for it |
| `--url` | Stash's GraphQL address (default `http://localhost:9999/graphql`, or `$STASH_URL`) |
| `--api-key` | Needed if Stash has a password: Settings → Security → API Key (or `$STASH_API_KEY`) |
| `--path-map LOCAL=STASH` | When Stash sees the files under a different path, e.g. in Docker; repeatable |
| `--organized` | Also mark the items as organized in Stash |
| `--studio`, `--tag-prefix`, `--no-tags` | Change the studio and the tag prefix for every site, or turn the tags off |

### Stash in Docker

If OF-Scraper saved files under `D:\OnlyFans` and Stash's container mounts that folder as `/data`:

```sh
python -m ofscraper.commands.stash_sync "<profile>/.data" --apply --path-map "D:\OnlyFans=/data"
```

A Windows `LOCAL` path ignores case and accepts `/` or `\`. Other paths must match exactly. Without the right mapping Stash can't find any of the files; the report says so in a `hint`, and nothing is created.

***

## Notes

* **Downloaded files only:** Only files OF-Scraper marked as downloaded are matched, by their exact path. Files you've moved or renamed since won't be found.
* **Files posted more than once:** A file posted in multiple places (for example in a message and again as a purchase) gets one item in Stash with the earliest date and all of its tags.
* **Performer matching:** Performers are matched by name (the username), ignoring case and by alias. A performer you created under another name gets a second one; merge them in Stash.
* **Finding Fansly galleries again:** A Fansly gallery is found again by its code (the post or message ID), so you can move it to another studio. Changing a gallery's code makes the next run create a new one.

The full details are in [`STASH.md`](https://github.com/cloakedkeys/OF-Scraper-Community/blob/main/STASH.md) in the fork.
