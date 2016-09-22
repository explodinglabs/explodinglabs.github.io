---
layout: post
title: "JSON-RPC in Python with aiohttp"
date: 2016-08-01
permalink: /jsonrpc/aiohttp
comments: true
---
<div class="wide-logos" markdown="1">
![flask](/assets/aiohttp.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build an [aiohttp](http://aiohttp.readthedocs.io/) server to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install the dependencies — aiohttp to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```shell
$ pip install aiohttp jsonrpcserver
```
Create a `server.py`:

```python
from aiohttp import web
from jsonrpcserver import Methods, dispatch

methods = Methods()
@methods.add
def ping():
    return 'pong'

async def handle(request):
    request = await request.text()
    response = dispatch(methods, request)
    return web.json_response(response)

app = web.Application()
app.router.add_post('/', handle)

if __name__ == '__main__':
    web.run_app(app, port=5000)
```
Start the server:

```shell
$ python server.py
======== Running on http://0.0.0.0:5000/ ========
(Press CTRL+C to quit)
```

Client
======
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

```shell
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
