---
layout: post
title: "JSON-RPC over ZeroMQ in Python with PyZMQ"
date: 2016-08-01
permalink: /jsonrpc/pyzmq
comments: true
---
{::options syntax_highlighter_opts="default_lang: python" /}

We'll build a [ZeroMQ](http://zeromq.org) server in Python, taking JSON-RPC
requests on port 5000. It should respond to "ping" with "pong".

Server
======

``` shell
$ pip install pyzmq jsonrpcserver
$ cat server.py
```
```python
import zmq
from jsonrpcserver import dispatch

def ping():
    return 'pong'

context = zmq.Context()
socket = context.socket(zmq.REP)
socket.bind('tcp://*:5000')

while True:
    request = socket.recv().decode('UTF-8')
    response = dispatch([ping], request)
    socket.send_string(str(response))
```
``` shell
$ python ./server.py
```

Client
======

``` shell
$ pip install jsonrpcclient pyzmq
$ python
```
```python
>>> from jsonrpcclient.zmq_server import ZMQServer
>>> ZMQServer('tcp://localhost:5000').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```
