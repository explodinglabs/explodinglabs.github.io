---
layout: post
title: "JSON-RPC in Python with Tornado"
date: 2016-09-13
permalink: /jsonrpc/tornado
comments: true
---
<div class="wide-logos" markdown="1">
![tornado](/assets/tornado.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build an [Tornado](http://www.tornadoweb.org/) server to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install the dependencies — Tornado to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```sh
$ pip install tornado jsonrpcserver
```
Create a `server.py`:

```python
from tornado import ioloop, web
from jsonrpcserver.aio import methods

@methods.add
async def ping():
    return 'pong'

class MainHandler(web.RequestHandler):
    async def post(self):
        request = self.request.body.decode()
        response = await methods.dispatch(request)
        self.write(response)

app = web.Application([(r"/", MainHandler)])

if __name__ == '__main__':
    app.listen(5000)
    ioloop.IOLoop.current().start()
```
Start the server:

```sh
$ python server.py
```

Synchronous client
==================

Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests.

```sh
$ pip install 'jsonrpcclient[requests]'
$ python
```
```python
>>> from jsonrpcclient.http_client import HTTPClient
>>> HTTPClient('http://localhost:5000/').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1} (200 OK)
'pong'
```

Asynchronous client with Tornado
================================

We can send asynchronous requests in Tornado with jsonrpcclient (thanks to
[saaj](https://github.com/saaj/)):

```sh
$ pip install 'jsonrpcclient[tornado]'
```
Create a `client.py`:

```python
from tornado import ioloop
from jsonrpcclient.tornado_client import TornadoClient

client = TornadoClient('http://localhost:5000/')

async def main():
    result = await client.request('ping')
    print(result)

ioloop.IOLoop.current().run_sync(main)
```
The `async`/`await` syntax requires Python 3.5+. Prior to that use
[@gen.coroutine and
yield](http://tornado.readthedocs.io/en/stable/guide/coroutines.html#python-3-5-async-and-await).

```sh
$ python client.py
INFO:jsonrpcclient.client.request:{"jsonrpc": "2.0", "method": "ping", "id": 1}
INFO:jsonrpcclient.client.response:{"jsonrpc": "2.0", "result": "pong", "id": 1}
pong
```
