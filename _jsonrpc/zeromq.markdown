---
layout: post
title: "JSON-RPC in Python over ZeroMQ"
date: 2016-08-01
permalink: /jsonrpc/zeromq
comments: true
---
{::options syntax_highlighter_opts="default_lang: python" /}

<div style="float: right; margin-left: 1em;" markdown="1">
![zeromq](/assets/zeromq.jpg)
</div>

We'll build a [ZeroMQ](http://zeromq.org) server in Python, taking JSON-RPC
requests on port 5000. It should respond to "ping" with "pong".

Install the dependencies — [pyzmq](https://pyzmq.readthedocs.io/) to take
requests and [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process
them:

``` shell
$ pip install pyzmq jsonrpcserver
```
Create a `server.py`:

```python
import zmq
from jsonrpcserver import Methods, dispatch

methods = Methods()
@methods.add
def ping():
    return 'pong'

context = zmq.Context()
socket = context.socket(zmq.REP)

if __name__ == '__main__':
    socket.bind('tcp://*:5000')
    while True:
        request = socket.recv().decode()
        response = dispatch(methods, request)
        socket.send_string(str(response))
```
Start the server:

``` shell
$ python ./server.py
```

Client
======
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

``` shell
$ pip install 'jsonrpcclient[pyzmq]'
$ python
```
```python
>>> from jsonrpcclient.zmq_client import ZMQClient
>>> ZMQClient('tcp://localhost:5000').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```
