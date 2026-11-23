# Username selection or Fuzzy Search

> ℹ️ Fuzzy search is built to mimic `fzf`.

OF-Scraper uses fuzzy search to make selecting creators easier. It finds close matches for the text you type.

***

## Selecting a model

| Action | Keys |
|---|---|
| Toggle the highlighted creator | `End`, `Home`, `PageUp`, `PageDown`, `Shift+Right` |
| Toggle and move down / up | `Tab` / `Shift+Tab` |
| Select all, or clear all if all are already selected | `Ctrl+A` |
| Select all | `Ctrl+S` |
| Clear all | `Ctrl+D` |
| Range select or deselect | `Alt+B` |
| Move | `Up`/`Down`, `Ctrl+P`/`Ctrl+N` |
| Filter | Type text (`Space` types a space; it doesn't toggle) |
| Show full details of a creator | `Alt+D` |
| Change sort and filters | `Alt+X` or `Ctrl+B` |
| Show the key help | `Alt+V` or `Ctrl+V` |
| Confirm | `Enter` |
| Go back | `Esc` |

`Ctrl+A`, `Ctrl+S`, and `Ctrl+D` only affect the creators the current filter shows.

***

## Getting Model Detail

Only a limited amount of data can be shown at a time, as the prompt menu doesn't work well when entries exceed a single line.

To view all details for a creator, press `Alt+D`.

***

## Sorting/Filtering List

Adjust the filters that control which creators appear in the list and how they're sorted:

`Alt+X` or `Ctrl+B`

***

## Searching the list

Start typing to filter the list (for example, `example`). The results depend on your account and active filters.

![image](https://user-images.githubusercontent.com/67020411/230736225-1b24a4b3-d56f-4297-88bd-63e2d4815990.png)

Entering `1` filters out non-matching options, displaying only `1`:

![image](https://user-images.githubusercontent.com/67020411/230736203-c7e433f9-30a9-4c35-8615-8046b3d7d001.png)

### How does searching affect my currently selected creators?

It doesn't; it only affects which creators appear in the list. For example:

![image](https://user-images.githubusercontent.com/67020411/230736111-3581cc77-bca0-491f-b86c-fdd3bd1d6551.png)

![image](https://user-images.githubusercontent.com/67020411/230736159-bdc9f4ec-87d7-48ac-9099-81743b52c785.png)

In the second image, although previously chosen options aren't visible, they're still selected, as shown by the count in parentheses (`3`).

***

## Unselecting

To unselect a creator, either clear the search filter or type a filter that shows that creator, then use the toggle keys above. To clear all currently shown creators at once, press `Ctrl+D`.

***

## More Controls

Controls may change, and additional keys may not be listed here. Press `Alt+V` or `Ctrl+V` during creator selection to view the current key bindings.
