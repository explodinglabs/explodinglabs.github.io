---
layout: post
date: 2018-03-23
title: Convert Python dict to an object with attributes
category: python
image: /assets/python-wide.png
redirect_from:
    - /airflow/testing-operators
    - /airflow/testing-airflow-operators
---
<div class="wide-logos" markdown="1">
![airflow](/assets/python.png)
</div>

## Convert a dict to a mutable object

Use `types.SimpleNamespace`.

```python
>>> my_dict = {'name': 'foo', 'value': 1}
>>> from types import SimpleNamespace
>>> obj = SimpleNamespace(**my_dict)
>>> obj.name
'foo'
```

## Convert a dict to an immutable object

Use `collections.namedtuple`.

```python
>>> from collections import namedtuple
>>> obj = namedtuple('Obj', my_dict.keys())(**my_dict)
>>> obj.name
'foo'
```
