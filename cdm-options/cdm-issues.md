# Manual CDM issues

Problems you may see when using your own CDM files (`--key-mode manual`).

## "Descriptors cannot not be created directly" (protobuf error)

DRM videos fail, and the log shows:

```
TypeError: Descriptors cannot not be created directly.
If this call came from a _pb2.py file, your generated code is out of date and
must be regenerated with protoc >= 3.19.0.
If you cannot immediately regenerate your protos, some other possible workarounds are:

 1. Downgrade the protobuf package to 3.20.x or lower.
 2. Set PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python (but this will use pure-Python parsing and will be much slower).
```

**What it means:** the manual CDM uses `pywidevine`, which relies on the `protobuf` package. The error appears when an old `pywidevine` is installed next to a newer `protobuf` that it wasn't built for.

**How to fix it:**

1. Reinstall OF-Scraper the way the [install guide](../installation/README.md) describes. The fork pins versions that work together (`pywidevine` 1.9 with a current `protobuf`), so a clean install doesn't hit this error. The Docker images and release binaries already include them.
2. If you can't reinstall yet, set the environment variable `PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python` before running OF-Scraper. It works around the error, but decoding is slower.

Background: [VideoHelp forum thread](https://forum.videohelp.com/threads/408031-Dumping-Your-own-L3-CDM-with-Android-Studio/page9#post2697726).
