---
layout: post
title: "Pylint: Disable all errors except one"
date: 2017-10-16
permalink: /pylint/disable-all-except-one
comments: true
---

For example, to show only *unused imports*:

```zsh
pylint --disable=all --enable=unused-import directory
```
