---
layout: post
title: "JSON-RPC in Python with Websockets"
date: 2016-09-23
permalink: /jsonrpc/websockets
comments: true
---
<div class="wide-logos" markdown="1">
![websockets](/assets/websockets.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build a Websockets server to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install the dependencies —  [websockets](http://websockets.readthedocs.io/) to
take requests and [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to
process them:

```sh
$ pip install websockets jsonrpcserver
```
Create a `server.py`:

```python
import asyncio
import websockets
from jsonrpcserver.aio import methods

@methods.add
async def ping():
    return 'pong'

async def main(websocket, path):
    request = await websocket.recv()
    response = await methods.dispatch(request)
    await websocket.send(str(response))

start_server = websockets.serve(main, 'localhost', 5000)
asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()
```
Start the server:

```sh
$ python server.py
```

Client
======
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

```sh
$ pip install 'jsonrpcclient[websockets]'
```
Create a `client.py`:

```python
import asyncio
import websockets
from jsonrpcclient.websockets_client import WebSocketsClient

async def main():
    async with websockets.connect('ws://localhost:5000') as ws:
        response = await WebSocketsClient(ws).request('ping')
        print(response)

asyncio.get_event_loop().run_until_complete(main())
```
Run the client:

```sh
$ python client.py
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
pong
```
