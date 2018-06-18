---
layout: post
category: python
date: 2018-03-23
title: Convert a dictionary to postfix notation
image: /assets/python-wide.png
permalink: /python/convert-dict-to-postfix-notation
redirect_from:
    - /convert-dict-to-postfix-notation
    - /python/convert-dict-to-object-with-attributes
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

We have a dictionary, and want to convert it to a an object with postfix
notation ('obj.name').

## Convert to an immutable object

Use `collections.namedtuple`.

```python
>>> from collections import namedtuple
>>> data = {'id': 1, 'name': 'foo'}
>>> Obj = namedtuple('Obj', data.keys())
>>> obj = Obj(**data)
>>> obj.name
'foo'
```

## Convert to a mutable object

Use `types.SimpleNamespace`.

```python
>>> from types import SimpleNamespace
>>> data = {'id': 1, 'name': 'foo'}
>>> obj = SimpleNamespace(**data)
>>> obj.name
'foo'
```

See also: [Convert a sequence to postfix notation](/convert-sequence-to-postfix-notation)
