---
layout: post
title: "JSON-RPC over Socket.io in Python with Flask-SocketIO"
date: 2016-08-01
permalink: /python/flask-socketio/jsonrpc
---

How to create a socket.io server to handle JSON-RPC requests on port
5000. The server should respond with "pong" when it receives "ping".

* TOC
{:toc}

Server
======

Install dependencies
--------------------

```shell
$ pip install flask-socketio eventlet jsonrpcserver
```

Write server script
-------------------

Create a `server.py`:

```python
import logging
from flask import Flask
from flask_socketio import SocketIO, send
from jsonrpcserver import dispatch

logging.getLogger('jsonrpcserver').setLevel(logging.INFO)
logging.getLogger('jsonrpcserver').addHandler(logging.StreamHandler())

app = Flask(__name__)
app.config['SECRET_KEY'] = 'secret!'
socketio = SocketIO(app)

def ping():
    return 'pong'

@socketio.on('message')
def handle_message(request):
    return dispatch([ping], request)

if __name__ == '__main__':
    socketio.run(app, port=5000)
```

Start the server
----------------

```shell
$ python server.py
(27985) wsgi starting up on http://127.0.0.1:5000
```

Client
======

Create `index.html` which is just a simple button:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"></script>
        <script type="text/javascript" src="http://cdnjs.cloudflare.com/ajax/libs/socket.io/1.4.5/socket.io.min.js"></script>
        <script type="text/javascript" src="client.js"></script>
    </head>
    <body>
        <button>Ping</button>
    </body>
</html>
```

Create ``client.js``:

```javascript
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
```

Running
-------

1. Launch index.html in a web browser.
2. Open the javascript console.
3. Click the Ping button.
