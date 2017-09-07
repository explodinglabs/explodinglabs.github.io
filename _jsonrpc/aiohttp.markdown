---
layout: post
title: "JSON-RPC in Python with aiohttp"
date: 2016-09-23
permalink: /jsonrpc/aiohttp
comments: true
---
<div class="wide-logos" markdown="1">
![flask](/assets/aiohttp.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll use [aiohttp](http://aiohttp.readthedocs.io/) to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install aiohttp to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```sh
$ pip install aiohttp jsonrpcserver
```
Create a `server.py`:

```python
from aiohttp import web
from jsonrpcserver.aio import methods

@methods.add
async def ping():
    return 'pong'

async def handle(request):
    request = await request.text()
    response = await methods.dispatch(request)
    if response.is_notification:
        return web.Response()
    else:
        return web.json_response(response, status=response.http_status)

app = web.Application()
app.router.add_post('/', handle)

if __name__ == '__main__':
    web.run_app(app, port=5000)
```
Start the server:

```sh
$ python server.py
======== Running on http://0.0.0.0:5000/ ========
(Press CTRL+C to quit)
```

Synchronous client
==================
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

```sh
$ pip install 'jsonrpcclient[requests]'
$ python
```
```python
>>> import jsonrpcclient
>>> jsonrpcclient.request('http://localhost:5000/', 'ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1} (200 OK)
'pong'
```

Asynchronous client with aiohttp
================================
```sh
$ pip install 'jsonrpcclient[aiohttp]'
```
Create a `client.py`:

```python
import aiohttp
import asyncio
from jsonrpcclient.aiohttp_client import aiohttpClient

async def main(loop):
    async with aiohttp.ClientSession(loop=loop) as session:
        client = aiohttpClient(session, 'http://localhost:5000/')
        response = await client.request('ping')
        print(response)

loop = asyncio.get_event_loop()
loop.run_until_complete(main(loop))
```
```sh
$ python client.py
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```
