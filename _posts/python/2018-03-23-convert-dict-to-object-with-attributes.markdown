---
layout: post
category: python
date: 2018-03-23
title: Convert Python dictionary to an object with attributes
image: /assets/python-wide.png
redirect_from:
    - /airflow/testing-operators
    - /airflow/testing-airflow-operators
---
<div class="wide-logos" markdown="1">
![airflow](/assets/python.png)
</div>

## Convert to a mutable object

Use `types.SimpleNamespace`.

```python
>>> from types import SimpleNamespace
>>> my_dict = {'name': 'foo', 'value': 1}
>>> obj = SimpleNamespace(**my_dict)
>>> obj.name
'foo'
```

## Convert to an immutable object

Use `collections.namedtuple`.

```python
>>> from collections import namedtuple
>>> my_dict = {'name': 'foo', 'value': 1}
>>> obj = namedtuple('Obj', my_dict.keys())(**my_dict)
>>> obj.name
'foo'
```
