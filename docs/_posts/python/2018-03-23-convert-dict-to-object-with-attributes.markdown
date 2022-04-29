---
layout: post
category: python
title: How to convert a Python dictionary to postfix notation?
image: /assets/python-wide.png
permalink: /python/convert-dict-to-postfix-notation
redirect_from:
    - /convert-dict-to-postfix-notation
    - /python/convert-dict-to-object-with-attributes
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

<div id="intro" markdown="1">
We have a dictionary, and want to convert it to a an object with postfix
notation like `obj.name`.
</div>

## Convert to an immutable object

Use `collections.namedtuple`.

```python
>>> from collections import namedtuple
>>> data = {"id": 1, "name": "foo"}
>>> namedtuple("Obj", data.keys())(**data)
Obj(id=1, name='foo')
```

## Convert to a mutable object

Use `types.SimpleNamespace`.

```python
>>> from types import SimpleNamespace
>>> SimpleNamespace(**{"id": 1, "name": "foo"})
namespace(id=1, name="foo")
```

See also: [Convert a sequence to postfix notation](/convert-sequence-to-postfix-notation)
