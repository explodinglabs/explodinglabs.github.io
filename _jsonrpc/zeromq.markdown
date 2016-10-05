---
layout: post
title: "JSON-RPC in Python over ZeroMQ"
date: 2016-08-01
permalink: /jsonrpc/zeromq
redirect_from: /jsonrpc/pyzmq
comments: true
---
<div class="wide-logos" markdown="1">
![zeromq](/assets/zeromq.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build a [ZeroMQ](http://zeromq.org) server to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install the dependencies — [pyzmq](https://pyzmq.readthedocs.io/) to take
requests and [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process
them:

``` shell
$ pip install pyzmq jsonrpcserver
```
Create a `server.py`:

```python
import zmq
from jsonrpcserver import methods

socket = zmq.Context().socket(zmq.REP)

@methods.add
def ping():
    return 'pong'

if __name__ == '__main__':
    socket.bind('tcp://*:5000')
    while True:
        request = socket.recv().decode()
        response = methods.dispatch(request)
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
>>> from jsonrpcclient.zeromq_client import ZeroMQClient
>>> ZeroMQClient('tcp://localhost:5000').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```

You can also do this [asynchronously](./zeromq-async) with Python 3.5+.
