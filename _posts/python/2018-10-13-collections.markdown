---
layout: post
category: python
date: 2018-10-13
title: "Python's collections"
permalink: /python/collections
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

These are the most commonly used collections:

|          | Immutable         | Mutable         |
|----------|-------------------|-----------------|
| Set      | frozenset         | set             |
| Sequence | tuple, str, bytes | list, bytearray |
| Mapping  |                   | dict            |

Or shown in a heirarchy:

## Set

- frozenset
- MutableSet
    - set

## Sequence
- tuple
- str
- ByteString
    - bytes
    - bytearray
- MutableSequence
    - list
    - bytearray

## Mapping
- MutableMapping
    - dict
