---
layout: post
title: "Pytest: How to xfail on a specific exception?"
category: python
permalink: /python/pytest-xfail-on-specific-exception
---

Use `@pytest.xfail` with the `raises` param.

```python
from pytest import mark

@mark.xfail(raises=RuntimeError)
def test_function_call() -> None:
    ...
```
