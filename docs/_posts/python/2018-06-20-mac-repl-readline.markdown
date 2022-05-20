---
layout: post
category: python
title: How to use Readline in the Python REPL on MacOS?
image: /assets/python-wide.png
permalink: /python/mac-repl-readline
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

<div id="intro" markdown="1">
How to use readline in the Python interactive interpreter on Mac.
</div>

Install the gnureadline Python package:
```sh
pip install gnureadline
```

Create a `~/.pythonstartup.py` script:
```python
import atexit
import gnureadline as readline
import logging
import os
import sys

logger = logging.getLogger(__name__)
logger.addHandler(logging.StreamHandler())
logger.setLevel(logging.INFO)

# Enable Tab Completion. OSX's bind should only be applied with legacy readline.
readline.parse_and_bind(
    "bind ^I rl_complete"
    if sys.platform == "darwin" and "libedit" in readline.__doc__
    else "tab: complete"
)

# Enable History File
history_file = os.environ.get(
    "PYTHON_HISTORY_FILE", os.path.join(os.environ["HOME"], ".pythonhistory")
)
if os.path.isfile(history_file):
    readline.read_history_file(history_file)
else:
    open(history_file, "a").close()
atexit.register(readline.write_history_file, history_file)

logger.info("Booted ~/.pythonstartup.py.")
```

Set the `PYTHONSTARTUP` env var:
```sh
export PYTHONSTARTUP=$HOME/.pythonstartup.py
```

Start the Python REPL.
```sh
$ python
Python 3.6.5 (default, Mar 29 2018, 15:37:32)
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.39.2)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
Booted pythonstartup.py.
>>>
```
