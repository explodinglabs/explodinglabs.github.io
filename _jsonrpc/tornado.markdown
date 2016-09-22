---
layout: post
title: "JSON-RPC in Python with Tornado"
date: 2016-09-13
permalink: /jsonrpc/tornado
comments: true
---
<div style="float: right" markdown="1">
![tornado](/assets/tornado.png)
</div>

Server
======
We'll build an HTTP server with Tornado, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port 5000. It should respond to
"ping" with "pong".

Install the dependencies — [Tornado](http://www.tornadoweb.org/) to take
requests and [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process
them:

```shell
$ pip install tornado jsonrpcserver
```
Create a `server.py`:

```python
from tornado import ioloop, web
from jsonrpcserver import Methods, dispatch

methods = Methods()
@methods.add
def ping():
    return 'pong'

class MainHandler(web.RequestHandler):
    def post(self):
        response = dispatch(methods, self.request.body.decode())
        self.write(response)

app = web.Application([(r"/", MainHandler)])

if __name__ == '__main__':
    app.listen(5000)
    ioloop.IOLoop.current().start()
```
Start the server:

```shell
$ python server.py
```

Client
======

Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests.

Synchronous
-----------
```shell
$ pip install 'jsonrpcclient[requests]'
$ python
```
```python
>>> from jsonrpcclient.http_client import HTTPClient
>>> HTTPClient('http://localhost:5000/').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```

Asynchronous with Tornado
-------------------------
We can send asynchronous requests in Tornado with jsonrpcclient (Thanks to
[saaj](https://github.com/saaj/)):

```shell
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
Note the `async`/`await` syntax requires Python 3.5+. Prior to that use
[@gen.coroutine and
yield](http://tornado.readthedocs.io/en/stable/guide/coroutines.html#python-3-5-async-and-await).


```shell
$ python client.py
INFO:jsonrpcclient.client.request:{"jsonrpc": "2.0", "method": "ping", "id": 1}
INFO:jsonrpcclient.client.response:{"jsonrpc": "2.0", "result": "pong", "id": 1}
pong
```
