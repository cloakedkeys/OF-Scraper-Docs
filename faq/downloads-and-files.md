# Downloads & Files

## Lots of tempvideo or tempaudio files

Make sure your CDM (Content Decryption Module) is set up correctly and `ffmpeg` 6 or newer is installed. Manual CDM is recommended.

See [CDM Options](../cdm-options/README.md).

***

## Files download fine but are counted as "failed"

Fixed in 3.15.0. This mostly happened when saving to a mapped or network drive. Update to the latest version.

***

## Two files saved with the same name overwrote each other

Newer versions save the second one as `name_<media_id>` instead. To recover files lost to this in older versions, see [Recover Filename Collisions](../using-the-scraper/recipes/recover-filename-collisions.md).

***

## Files skipped by the size limits or skip script come back

That's intended from 3.16.6: a skip is for this run only, so the file is tried again next run. To skip a file for good, have the skip download script print `skip-permanent`. See [Script Options](../getting-started/config-options/script-options.md).

***

## Support For Network Drives

Network drives have limited support for storing media, and aren't supported at all for config files or databases. Store config files and databases on a local drive.
