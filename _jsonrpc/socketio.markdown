---
layout: post
title: "JSON-RPC in Python over Socket.io"
date: 2016-08-01
permalink: /jsonrpc/flask-socketio
comments: true
---
We'll build a socket.io server in Python, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port
5000. It should respond to "ping" with "pong".

Install the dependencies —
[Flask-SocketIO](https://flask-socketio.readthedocs.org/) to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```shell
$ pip install flask-socketio eventlet jsonrpcserver
```
Create a `server.py`:

```python
from flask import Flask
from flask_socketio import SocketIO
from jsonrpcserver import Methods, dispatch

app = Flask(__name__)

methods = Methods()
@methods.add
def ping():
    return 'pong'

socketio = SocketIO(app)
@socketio.on('message')
def handle_message(request):
    return dispatch(methods, request)

if __name__ == '__main__':
    socketio.run(app, port=5000)
```
Start the server:

```shell
$ python server.py
(27985) wsgi starting up on http://127.0.0.1:5000
```

Client
======
Create an `index.html`:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
        <script type="text/javascript" src="http://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.min.js"></script>
        <script type="text/javascript">
$(function() {
    // Connect
    var socket = io.connect('http://localhost:5000/');
    // Connected
    socket.on('connect', function() {
        console.log('Connected');
    });
    // Send
    $('button').click(function(e) {
        message = {jsonrpc: "2.0", method: "ping", id: 1};
        console.log('--> '+JSON.stringify(message));
        socket.send(message, function(response) {
            console.log('<-- '+JSON.stringify(response));
        });
    });
});
        </script>
    </head>
    <body>
        <button>Ping</button>
    </body>
</html>
```

Running
-------

1. Launch index.html in a web browser.
2. Open the javascript console.
3. Click the Ping button.
