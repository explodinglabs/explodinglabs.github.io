---
layout: post
category: python
title: Python's collections
permalink: /python/collections
sitemap: false
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

These are the most commonly used collections:

|          | Immutable         | Mutable         |
|----------|-------------------|-----------------|
| Sequence | tuple, str, bytes | list, bytearray |
| Set      | frozenset         | set             |
| Mapping  |                   | dict            |

Or shown in a heirarchy:

## Sequence
- tuple
- str
- ByteString
    - bytes
    - bytearray
- MutableSequence
    - list
    - bytearray

## Set

- frozenset
- MutableSet
    - set

## Mapping
- MutableMapping
    - dict
