---
layout: page
title: "JSON-RPC over ZeroMQ in Python"
permalink: /python/jsonrpc/zeromq
---
{::options syntax_highlighter_opts="default_lang: python" /}

* TOC
{:toc}

Server
======

The server will handle incoming JSON-RPC requests on port 5555.
When it receives "ping", it should respond with "pong".

Install requirements
--------------------

``` shell
$ pip install pyzmq jsonrpcserver
```

Write server script
-------------------

Create a `server.py`:

    import zmq
    from jsonrpcserver import dispatch

    def ping():
        return 'pong'

    context = zmq.Context()
    socket = context.socket(zmq.REP)
    socket.bind('tcp://*:5555')

    while True:
        request = socket.recv().decode('UTF-8')
        response = dispatch([ping], request)
        socket.send_string(str(response))

Start the server
----------------

``` shell
$ python ./server.py
```

Client
======

Install requirements
--------------------

``` shell
$ pip install pyzmq jsonrpcclient
```

Ping the server
---------------

Send a JSON-RPC "ping" method to the server:

    >>> from jsonrpcclient.zmq_server import ZMQServer
    >>> ZMQServer('tcp://localhost:5555').request('ping')
    'pong'
