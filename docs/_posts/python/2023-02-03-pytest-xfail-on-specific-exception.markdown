---
layout: post
title: "Pytest: How to xfail on a specific exception?"
permalink: /python/pytest-xfail-on-specific-exception
---
Pytest's `xfail` decorator is useless becauses it expects the test to fail for
any reason, i.e. it expects an exception to be raised, but _any exception_ will
do.

To expect failure on a specific exception only, use `try/except` with the
`pytest.xfail` function:

```python
from pytest import xfail

def test_function_call() -> None:
    try:
        function_call()
    except ValueError:
        xfail("The function fails due to ...")
        raise
```
