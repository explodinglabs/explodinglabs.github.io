---
layout: post
title: "Pytest: How to expect a test to fail with a specific exception?"
category: python
permalink: /python/pytest-xfail-on-specific-exception
---

Use `@pytest.xfail` with the `raises` param.

```python
from pytest import mark

@mark.xfail(raises=RuntimeError)
def test_func() -> None:
    func()
```

This lets you expect a specific exception, but it won't let you say _where_ it should happen in the test.

In my opinion Pytest should provide a context manager, e.g.

```python
# DOES NOT WORK
def test_func() -> None:
    with xfail(raises=RuntimeError):
        func()
```
