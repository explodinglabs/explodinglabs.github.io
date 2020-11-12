---
layout: post
category: jsonrpc
title: JSON-RPC in Python with Websockets
permalink: /jsonrpc/websockets
---
<div class="wide-logos" markdown="1">
![websockets](/assets/websockets.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll use Websockets to take [JSON-RPC](http://www.jsonrpc.org/) requests. It
should respond to "ping" with "pong".

Install [websockets](http://websockets.readthedocs.io/) to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```sh
$ pip install websockets jsonrpcserver
```
Create a `server.py`:

```python
import asyncio
import websockets
from jsonrpcserver import method, async_dispatch as dispatch

@method
async def ping():
    return "pong"

async def main(websocket, path):
    response = await dispatch(await websocket.recv())
    if response.wanted:
        await websocket.send(str(response))

start_server = websockets.serve(main, "localhost", 5000)
asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()
```
Start the server:

```sh
$ python server.py
```

## Client

Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

```sh
$ pip install "jsonrpcclient[websockets]"
```
Create a `client.py`:

```python
import asyncio
import websockets
from jsonrpcclient.clients.websockets_client import WebSocketsClient

async def main():
    async with websockets.connect('ws://localhost:5000') as ws:
        response = await WebSocketsClient(ws).request('ping')
        print(response)

asyncio.get_event_loop().run_until_complete(main())
```
Run the client:

```sh
$ python client.py
pong
```
