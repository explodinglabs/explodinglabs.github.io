---
layout: post
category: python
title: Use Python virtual environments
permalink: /python/virtualenv
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

## Setup

Install virtualenvwrapper.
```sh
PIP_REQUIRE_VIRTUALENV=false pip3 install --user --upgrade virtualenvwrapper
```

Add the following to your startup script (e.g. `~/.zshenv`, `~/.bashrc`):
```sh
export WORKON_HOME=~/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/opt/local/bin/python3.8
export VIRTUALENVWRAPPER_VIRTUALENV=/Users/beaubarker/Library/Python/3.8/bin/virtualenv
source /Users/beaubarker/Library/Python/3.8/bin/virtualenvwrapper.sh
```

Source your startup script to bring the changes into your environment:
```sh
source ~/.zshenv
```

I like to disallow Pip from working when no virtualenv is active. This way we
don't accidentally modify the global system. Add the following to your startup
script:
```sh
export PIP_REQUIRE_VIRTUALENV=true
```

## Usage

To create a virtualenv:
```sh
mkvirtualenv -p $(which python3.6) my_virtualenv
```

It's important to specify the specific Python version to use for your specific
project. Install multiple versions of Python into your system to use for
different projects.

The virtualenv is created and activated. Install packages into it.

```sh
pip install ...
```

To deactivate the virtualenv:
```
deactivate
```

To reactivate it:
```
workon my_virtualenv
```

To delete the virtualenv (must be inactive):
```
rmvirtualenv my_virtualenv
```
