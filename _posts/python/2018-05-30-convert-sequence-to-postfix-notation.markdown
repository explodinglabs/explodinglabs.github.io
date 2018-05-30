---
layout: post
category: python
date: 2018-05-30
title: Convert a sequence to postfix notation
image: /assets/python-wide.png
permalink: /convert-sequence-to-postfix-notation
---
<div class="wide-logos" markdown="1">
![airflow](/assets/python.png)
</div>

We have a sequence such as a tuple or list, and want to convert it to a an
object with named attributes in postfix notation ('obj.name').

## Convert to an immutable object

Use `collections.namedtuple`.

```python
>>> from collections import namedtuple
>>> data = (1, 'foo')
>>> Obj = namedtuple('Obj', ['id', 'name'])
>>> obj = Obj(*data)
>>> obj.name
'foo'
```

## Convert to a mutable object

Use `types.SimpleNamespace`.

```python
>>> from types import SimpleNamespace
>>> data = (1, 'foo')
>>> dictionary = dict(zip(['id', 'name'], data))
>>> obj = SimpleNamespace(**dictionary)
>>> obj.name
'foo'
```

See also: [Convert a dictionary to postfix notation](/convert-dict-to-postfix-notation)
