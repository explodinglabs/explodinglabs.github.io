---
layout: post
title: "Pylint: Disable all errors except one"
date: 2017-10-16
permalink: /pylint/disable-all-except-one
---

For example, to show only one error type, *unused imports*:

```zsh
pylint --disable=all --enable=unused-import my-file.py
```
