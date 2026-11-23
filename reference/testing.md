# Testing

The repository includes a test suite.

## Install

Install the test dependencies:

```sh
uv sync --extra test
```

## Running

Run the full test suite in parallel from the cloned repository (warnings count as failures):

```sh
python -m pytest -n auto test
```

For a faster local loop that skips the heaviest integration tests (subprocess, `ffmpeg`, real timeouts, and bulk DB runs):

```sh
python -m pytest -n auto -m "not slow" test
```
