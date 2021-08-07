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
[jsonrpcserver](https://www.jsonrpcserver.com/) to process them:

```sh
$ pip install websockets jsonrpcserver
```

Create a `server.py`:

```python
import asyncio

from jsonrpcserver import method, Success, Result, async_dispatch
import websockets


@method
async def ping() -> Result:
    return Success("pong")


async def main(websocket, path):
    if response := await async_dispatch(await websocket.recv()):
        await websocket.send(response)


start_server = websockets.serve(main, "localhost", 5000)
asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()
```

Start the server:

```sh
$ python server.py
```

## Client

Use [jsonrpcclient](https://www.jsonrpcclient.com/) to send requests:

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
