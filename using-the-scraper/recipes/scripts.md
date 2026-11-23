---
description: Example of scripts to change the program behaviour
---

# Scripts

> ⚠️ **Python auto-detection:** All files must end with `.py` to be auto-detected by OF-Scraper as a Python script.

## Naming Scripts

Configure these in the `naming_script` setting in `config.json`.

### rename jpeg to jpg

```python
import sys
import json
import pathlib
def main():
    input_json_str = sys.stdin.read()

    # 1. Parse the JSON string into a Python dictionary
    data = json.loads(input_json_str)
    # 2. Fix name
    dir=data["dir"]
    file=data["file"].replace("jpeg","jpg").strip()
    filename=str(pathlib.Path(dir,file))
    # 3. Print to stdout for output
    print(filename, file=sys.stdout)
    # 4. Print all information data to stderr
    print(filename, file=sys.stderr)
if __name__=="__main__":
    main()
```
