---
layout: post
title: "JSON-RPC in Python over ZeroMQ, asynchronously"
date: 2016-09-28
permalink: /jsonrpc/zeromq-async
comments: true
---
<div class="wide-logos" markdown="1">
![zeromq](/assets/zeromq.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build a [ZeroMQ](http://zeromq.org) server to take
[JSON-RPC](http://www.jsonrpc.org/) requests, and process them asynchronously
(the synchronous version is [here](./zeromq)). The server should respond to
"ping" with "pong".

Install the dependencies — [aiozmq](https://aiozmq.readthedocs.io/) to take
requests and [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process
them:

```sh
$ pip install aiozmq jsonrpcserver
```
Create a `server.py`:

```python
import asyncio
import aiozmq
import zmq
from jsonrpcserver.aio import methods

@methods.add
async def ping():
    return 'pong'

async def main():
    rep = await aiozmq.create_zmq_stream(zmq.REP, bind='tcp://*:5000')
    while True:
        request = await rep.read()
        response = await methods.dispatch(request[0].decode())
        rep.write((str(response).encode(),))

if __name__ == '__main__':
    asyncio.set_event_loop_policy(aiozmq.ZmqEventLoopPolicy())
    asyncio.get_event_loop().run_until_complete(main())
```
Start the server:

```sh
$ python server.py
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
