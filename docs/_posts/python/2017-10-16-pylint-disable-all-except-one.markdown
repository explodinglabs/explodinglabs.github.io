---
layout: post
category: python
title: How to use only one error type in Pylint?
permalink: /python/show-only-one-pylint-error
redirect_from:
    - /pylint/show-only-one-type
    - /pylint/disable-all-except-one
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

To disable all errors except one, for example, unused imports:

```zsh
pylint --disable=all --enable=unused-import my_file.py
```
