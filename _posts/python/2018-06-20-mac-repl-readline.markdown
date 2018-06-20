---
layout: post
category: python
date: 2018-06-20
title: Readline in the Python REPL on MacOS
image: /assets/python-wide.png
permalink: /python/mac-repl-readline
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

How to use readline in the Python interactive interpreter on Mac.

Install the gnureadline Python package:
```sh
pip install gnureadline
```

Create a `~/.pythonstartup.py` script:
```python
try:
    import readline
    import atexit
    import os
    import sys
    import platform
    import gnureadline as readline
except ImportError as exception:
    print('Shell Enhancement module problem: {0}'.format(exception))
else:
    # Enable Tab Completion
    # OSX's bind should only be applied with legacy readline.
    if sys.platform == 'darwin' and 'libedit' in readline.__doc__:
        readline.parse_and_bind("bind ^I rl_complete")
    else:
        readline.parse_and_bind("tab: complete")

    # Enable History File
    history_file = os.environ.get(
        "PYTHON_HISTORY_FILE", os.path.join(os.environ['HOME'],
        '.pythonhistory'))

    if os.path.isfile(history_file):
        readline.read_history_file(history_file)
    else:
        open(history_file, 'a').close()

    atexit.register(readline.write_history_file, history_file)
    print('Booted ~/pythonstartup.py.')
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
Booted ~/pythonstartup.py.
>>>
```
