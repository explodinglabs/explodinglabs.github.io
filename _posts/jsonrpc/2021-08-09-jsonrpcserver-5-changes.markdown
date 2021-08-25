---
layout: post
category: jsonrpc
title: Changes in Jsonrpcserver 5
permalink: /jsonrpcserver-5-changes
---
<div class="warning">
    <p>Jsonrpcserver 5 requires Python 3.8+.</p>
</div>

Jsonrpcserver is a Python library that dispatches JSON-RPC requests to your
Python code and gives you a JSON-RPC response.

Version 5 is a complete rebuild. The usage remains mostly the same except for a
few important changes. [Full version 5 documentation is
here](https://www.jsonrpcserver.com/en/latest/).

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/3_BMmgJaFHQ" frameborder="0" allowfullscreen></iframe>
</div>

## Methods return a Result

Writing a method is the same as before except for the return value which is now `Success` or `Error`.

```python
@method
def ping() -> Result:
    return Success("pong")
```

These return values are the [JSON-RPC responses objects](https://www.jsonrpc.org/specification#response_object) (minus
the "jsonrpc" and "id" parts, the library takes care of those for you).

## Dispatch returns JSON

Previously the `dispatch` function gave you an object which you had to apply
`str` to in order to get the json response. Now you just get the json
string.

```python
>>> dispatch('{"jsonrpc": "2.0", "method": "ping", "id": 1}')
'{"jsonrpc": "2.0", "result": "pong", "id": 1}'
```

For notifications you get an empty string. For async protocols (sockets,
message queues), [don't send the empty string
back](https://www.jsonrpcserver.com/en/latest/async.html#notifications).

## Logging removed

The library will no longer log requests and responses. Logging can be done by the
user, outside of the library. See [issue #152](https://github.com/explodinglabs/jsonrpcserver/issues/152).

## Configuration file removed

Version 4 allowed you to configure the library with a config file. This has
been removed. Pass arguments to `dispatch` instead.

## Options removed

The "trim log values" and "convert camel case" options have been removed.

## Methods collection is now a dict

There's an optional parameter to `dispatch` that lets you
specify a collection of methods to dispatch to. This parameter remains, but the value
which was previously an instance of a Methods class is now simply a `dict`.

```python
dispatch(request, methods={"ping": lambda: Success("pong")})
```
