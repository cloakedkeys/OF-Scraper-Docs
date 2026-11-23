---
description: Setting up authorization
---

# Auth

***

> ℹ️ **Still having authentication issues?** Open an issue in the fork's GitHub repository with a debug log attached. The session cookie is masked in logs.

> ℹ️ **This page is for OnlyFans.** For Fansly, see [Fansly](../fansly.md).

The auth file is `auth.json` in your profile folder (`~/.config/ofscraper/main_profile/` by default).

## Example

> ℹ️ Values are randomised, but should look similar in format to this example.

```json
{
    "auth": {
        "user_agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
        "x-bc": "fncx03r1ygvh26ezq4pe830l49xtj1a146e1x2av",
        "auth_id": "400000",
        "sess": "5pb18tyng144dqyzevbgfddnrz",
        "auth_uid": "400000"
    }
}
```

Older files with `auth_uid_` still work.

***

## Auto methods

You have two automatic options for fetching authentication info. If possible, use the cookie helper: it takes the least effort once set up.

### M-rcus Cookie Helper

Install the browser extension by following the instructions at [OnlyFans-Cookie-Helper](https://github.com/M-rcus/OnlyFans-Cookie-Helper).

![image](https://user-images.githubusercontent.com/67020411/230731183-26a43e62-4385-4fd9-aee8-f75a7c2d33cb.png)

With the helper installed, copy and paste its output into OF-Scraper.

### Browser Extraction

Not all fields can be extracted automatically with this method. You still need to copy the `x-bc` header and `User-Agent` manually (as shown below), but you don't need to extract any cookies.

![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/request_headers.png)

See the manual section below for how to find `x-bc` and `User-Agent`.

***

## Manual methods

> ℹ️ You can also edit auth information manually from inside OF-Scraper.

With this option, you enter all required fields manually:

```json
{
    "auth": {
        "sess": "",
        "auth_id": "",
        "auth_uid": "",
        "user_agent": "",
        "x-bc": ""
    }
}
```

#### Step One: Creating the 'auth.json' File

Run `ofscraper` in your terminal. Because no `auth.json` exists yet, OF-Scraper creates one and prompts you for your auth details.

#### Step Two: Getting Your Auth Info

> ℹ️ If you already used DIGITALCRIMINAL's OnlyFans script, you can copy and paste the auth information from there.

Go to your [OnlyFans notifications page](https://onlyfans.com/my/notifications) and open your browser's developer tools:

| Operating System | Shortcut |
|---|---|
| macOS | `Cmd + Opt + I` |
| Windows | `Ctrl + Shift + I` |
| Linux | `Ctrl + Shift + I` |

### 1. Getting a valid request

1. With developer tools open, your screen looks like this:

   ![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/browser_tools_open.png)

2. Click the **Network** tab:

   ![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/network_tab.png)

3. Click the **XHR** sub-tab inside **Network**:

   ![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/xhr_tab.png)

4. Refresh the page while developer tools stay open, then look for an entry named `init`:

   ![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/init.png)

5. Click `init` and make sure you're in the **Headers** section:

   ![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/headers.png)

If you found `init`, skip to step 2 below. Otherwise, see the fallback note next.

***

> ℹ️ If `init` doesn't appear, use any entry with the domain `onlyfans.com`.

#### **Examples**

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption><p>onlyfans.com</p></figcaption></figure>

You may need to right-click the table header row to enable the **Domain** column:

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

***

### 2. Getting data from requests

![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/init.png)

Scroll down to **Request Headers**. You'll see three fields: `Cookie`, `User-Agent`, and `x-bc`.

![](https://raw.githubusercontent.com/taux1c/onlyfans-scraper/main/media/request_headers.png)

Inside `Cookie`, look for:

* `sess=`
* `auth_id=`
* `auth_uid_=` *(only present if you have 2FA enabled; it has numbers after the final underscore and before `=`, which is your `auth_id`)*

For each cookie value, copy everything **after** `=` and **before** `;`.

Paste each value into OF-Scraper as prompted and press Enter:

1. `sess`
2. `auth_id`
3. `auth_uid` (**leave blank if you don't use 2FA**)
4. `User-Agent` (below `Cookie` in **Request Headers**)
5. `x-bc` (also in **Request Headers**)

You're now ready to use `ofscraper`.

Typing `quit` or `main` at an auth prompt exits or returns to the main menu. To make a run quit on an auth error instead of prompting, pass `--auth-fail`.
