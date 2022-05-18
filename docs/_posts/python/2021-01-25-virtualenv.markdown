---
layout: post
category: python
title: How to use Python virtual environments?
permalink: /python/virtualenv
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

Install
[Virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/).

Here's how I install it on Mac:

```sh
PIP_REQUIRE_VIRTUALENV=false pip3 install --user --upgrade virtualenvwrapper
```

Add the following to your startup script (e.g. `~/.zshenv`, `~/.bashrc`):
```sh
export PIP_REQUIRE_VIRTUALENV=true
export WORKON_HOME=~/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/opt/local/bin/python3.8
export VIRTUALENVWRAPPER_VIRTUALENV=~/Library/Python/3.8/bin/virtualenv
source ~/Library/Python/3.8/bin/virtualenvwrapper.sh
```

Source your startup script to bring the changes into your environment:
```sh
source ~/.zshenv
```

## Usage

The main two commands you need are `mkvirtualenv` and `workon`. 

To create a virtualenv:
```sh
mkvirtualenv -p $(which python3.6) my_virtualenv
```

It's important to specify the specific Python version to use for your specific
project. Install multiple versions of Python into your system to use for
different projects.

The virtualenv is created and activated.
You can install packages into it with `pip install`.

After creating the env, always follow with `setvirtualenvproject`, which tells the virtualenv to change into the current directory next time you work on this project.
```sh
setvirtualenvproject
```

Next time you want to work on the project:
```
workon my_virtualenv
```

To delete the virtualenv (must be inactive):
```
deactivate
rmvirtualenv my_virtualenv
```
