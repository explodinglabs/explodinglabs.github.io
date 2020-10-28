# apply_defaults

Apply a set of default values to a function's optional parameters, if not
passed.

Normally when calling a function, if a parameter isn't specified, the default
value from the parameter list is used.

These decorators add another layer; if the parameter isn't specified, _it tries
another set of values_, finally falling back to the default value.

The values can be a dictionary, a ConfigParser object, or the bound object.

It's useful for configuring your functions/application.

## apply_config

This decorator applies the options from a ConfigParser object:

```python
from apply_defaults import apply_config
from configparser import ConfigParser

config = ConfigParser()

@apply_config(config)
def my_func(foo=None)
    return foo
```

When a value is passed, take this value.

```python
>>> my_func(foo="bar")
'bar'
```

There is no configuration yet, so my_func takes the parameter's default value.

```python
>>> my_func()
None
```

With some configuration loaded, the param takes the value from the
configuration.

```python
>>> config.read_dict({"general": {"foo": "foo"}})
>>> my_func()
'foo'
```

## apply_self

This decorator applies values from the bound object:

```python
from apply_defaults import apply_self

class MyObject:
    def __init__(self):
        self.foo = "foo"

    @apply_self
    def method(self, foo=None):
        return foo
```

When a `foo` value is passed, take that.

```python
>>> MyObject().method(foo="bar")
'bar'
```

When a value is _not_ passed, `self.foo` is used.

```python
>>> MyObject().method()
'foo'
```
