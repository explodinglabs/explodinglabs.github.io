---
layout: post
category: python
title: "Writing parameters in a Python function signature"
permalink: /python/parameters
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

When writing parameters, we tend to ask:

_Is the parameter required, or can we use a default value?_

```python
def f(required, optional=None):
```

But there's another question to ask:

_Is its purpose obvious, or should it be named by the caller?_

Placing an asterisk `*` in the parameter list forces all of the parameters
following it to be named.

```python
def f(
    unnamed_or_named_and_required,
    unnamed_or_named_and_optional=None,
    *,
    named_and_required,
    named_and_optional=None
):
```

If we want to **catch** any other un-named parameters, use a variable name
following the asterisk (typically `*args`). This has the same effect as a
bare-asterisk `*`; _every parameter following it must be named_.

```python
def f(
    unnamed_or_named_and_required,
    unnamed_or_named_and_optional=None,
    *rest_of_unnamed,
    named_and_required,
    named_and_optional=None
):
```

To catch the rest of the *named* parameters, use double-asterisk with a name
(typically `**kwargs`). This must come last.

```python
def f(
    unnamed_or_named_and_required,
    unnamed_or_named_and_optional=None,
    *rest_of_unnamed,
    named_and_required,
    named_and_optional=None
    **rest_of_named
):
```

Unlike the single-asterisk, this catch-all can not be bare (`**`). It must be
given a name; it would have no purpose without one.

## Footnotes

When _calling_ a function or class, pass unnamed, then named, then unpack
unnamed, then unpack named.

```python
f(unnamed, named="foo", *unpack_unnamed, **unpack_named)
```

There are a couple of PEPs ([1](https://www.python.org/dev/peps/pep-0457/),
[2](https://www.python.org/dev/peps/pep-0570/)) proposing to add the
capability to force parameters to be un-named. This would take the parameter
groups to:

```python
def f(
    unnamed_and_required,
    unnamed_and_optional=None,
    /,
    unnamed_or_named_and_required,
    unnamed_or_named_and_optional=None,
    *rest_of_unnamed,
    named_and_required,
    named_and_optional=None
    **rest_of_named
):
```
