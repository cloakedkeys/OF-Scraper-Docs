---
description: Customise how the program formats filenames for downloaded content.
---

# Filename Modification Options

## Filename Modification Parameters

### -g, --original

* **Disables:** Truncation of long file paths.
* **Default:** `None` (paths are truncated by default).
* **Use case:** Keep the full original file path when you don't want names shortened.

### -tt, --text-type \[argument]

* **Sets:** The unit used to measure the maximum length of the filename text placeholder.
* **Possible choices:**
  * `word`: Splits the text placeholder into words (on `space_replacer`, or a space) and counts words.
  * `letter`: Counts the total number of characters in the text placeholder.
* **Default:** The `text_type_default` config setting (`letter` unless changed).
* **Example:** `-tt letter -tl 10` truncates the text placeholder to at most 10 characters.

### -sr, --space-replacer \[argument] (optional)

* **Replaces:** Spaces in the filename text with the given character.
* **Default:** `None` (spaces are kept as spaces).
* **Use case:** Useful for file systems or apps that don't handle spaces well.
* **Example:** `-sr _` replaces spaces with underscores (for example, `This File.txt` becomes `This_File.txt`).

### -tl, --textlength \[argument]

* **Sets:** The maximum length of the filename text placeholder.
* **Default:** `None` (no limit on text length).
* **Effect:** Truncates text placeholders that exceed the given length.
* **Use case:** Keeps filenames within OS character limits, which long post text can otherwise exceed.

**Note:**

* These options work together to shape the final filename.
* When truncation happens, it uses the `-tt` unit (`word` or `letter`), the `-tl` length and the current OS limits.
