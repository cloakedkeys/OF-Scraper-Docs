# Adding Proxy

Set the `OFSC_PROXY` environment variable (or add it to a `.env` file listed in `env_files`). There is no `config.json` key.

Only `http://` and `https://` proxies are supported; SOCKS proxies aren't supported.

For compatibility with `httpx` and `aiohttp`, include credentials in the proxy URL if required:

```text
OFSC_PROXY=http://username:password@localhost:8030
```
