---
layout: post
title: "JSON-RPC in Python over Socket.io"
date: 2016-08-01
permalink: /jsonrpc/socketio
redirect_from: /jsonrpc/flask-socketio
comments: true
---
<div class="wide-logos" markdown="1">
![socketio](/assets/socketio.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build a [Socket.IO](http://socket.io/) server to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install the dependencies —
[Flask](http://flask.pocoo.org),
[Flask-SocketIO](https://flask-socketio.readthedocs.org/) and
[eventlet](http://eventlet.net/) to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```sh
$ pip install flask flask-socketio eventlet jsonrpcserver
```
Create a `server.py`:

```python
from flask import Flask
from flask_socketio import SocketIO
from jsonrpcserver import methods

app = Flask(__name__)
socketio = SocketIO(app)

@methods.add
def ping():
    return 'pong'

@socketio.on('message')
def handle_message(request):
    return methods.dispatch(request)

if __name__ == '__main__':
    socketio.run(app, port=5000)
```
Start the server:

```sh
$ python server.py
(27985) wsgi starting up on http://127.0.0.1:5000
```

Client
======

TODO.
