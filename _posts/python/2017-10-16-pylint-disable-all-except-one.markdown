---
layout: post
category: python
date: 2017-10-16
title: "Pylint: Show only one error type"
permalink: /pylint/show-only-one-type
redirect_from: /pylint/disable-all-except-one
---
<div class="wide-logos" markdown="1">
![airflow](/assets/python.png)
</div>

To disable all errors except one, for example, *unused imports*:

```zsh
pylint --disable=all --enable=unused-import my_file.py
```
