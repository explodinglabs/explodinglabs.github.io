---
layout: post
title: Changes in jsonrpcserver 5
permalink: /jsonrpcserver-5-changes
---
Version 5 is a complete rebuild. The usage remains mostly the same except for
a few important changes.

## Methods return a Result

Writing a method is the same as before except for the return value.

You now return Success or Error.

```python
@method
def ping() -> Result:
    return Success("pong")
```

These return values are the JSON-RPC responses objects (see the 
[specification](https://www.jsonrpc.org/specification#response_object)), minus
the "jsonrpc" and "id" parts (the library takes care of those for you).

## Dispatch returns JSON

Previously the `dispatch` function gave you an object which you had to apply
`str()` to in order to get the json response. Now you just get the json
string.

```python
>>> dispatch('{"jsonrpc": "2.0", "method": "ping", "id": 1}')
'{"jsonrpc": "2.0", "result": "pong", "id": 1}'
```

For notifications you get an empty string. For async protocols (sockets,
message queues), [don't send the empty string
back](https://www.jsonrpcserver.com/en/latest/async.html#notifications).

## Methods collection is now a dict

There's an optional parameter to `dispatch` that lets you
specify a collection of methods to dispatch to. This parameter remains, but the value
which was previously an instance of a Methods class is now simply a `dict`.

```python
dispatch(request, methods={"ping": lambda: Success("pong")})
```

## Logging removed

The library will no longer log requests and responses. This can be done by the
user. See [issue #152](https://github.com/bcb/jsonrpcserver/issues/152).

## Configuration file removed

Version 4 allowed you to configure the library with a config file. This has
been removed. Pass arguments to `dispatch` instead.

## Options removed

The "trim log values" and "convert camel case" options have been removed.

