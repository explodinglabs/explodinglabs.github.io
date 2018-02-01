---
layout: post
title: "Pylint: Show only one error type"
date: 2017-10-16
permalink: /pylint/show-only-one-type
redirect_from: /pylint/disable-all-except-one
---
To disable all errors except one, for example, *unused imports*:

```zsh
pylint --disable=all --enable=unused-import my_file.py
```
