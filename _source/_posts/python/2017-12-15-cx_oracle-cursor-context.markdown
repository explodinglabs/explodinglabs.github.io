---
layout: post
category: python
title: cx_Oracle cursor context
permalink: /python/cx-oracle-cursor-context
redirect_from: /cx_oracle/cursor-context
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

Use `contextlib`'s `closing` context manager:

```python
from contextlib import closing
with closing(connection.cursor()) as cursor:
   # Use cursor here. Will close when it leaves the block.
```
