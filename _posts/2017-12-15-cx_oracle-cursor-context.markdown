---
layout: post
title: "cx_Oracle cursor context"
date: 2017-12-15
permalink: /cx_oracle/cursor-context
comments: true
---
Use `contextlib`'s `closing` context manager:

```python
from contextlib import closing
with closing(connection.cursor()) as cursor:
   # Use cursor here. Will close when it leaves the block.
```
