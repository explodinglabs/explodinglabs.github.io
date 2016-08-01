---
layout: post
title: "JSON-RPC over ZeroMQ in Python with PyZMQ"
date: 2016-08-01
permalink: /jsonrpc/pyzmq
comments: true
---
{::options syntax_highlighter_opts="default_lang: python" /}

We'll build a [ZeroMQ](http://zeromq.org) server in Python, taking JSON-RPC
requests on port 5000. It should respond to "ping" with "pong".

* TOC
{:toc}

Server
======

Install dependencies
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
    socket.bind('tcp://*:5000')

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

Install dependencies
--------------------

``` shell
$ pip install pyzmq jsonrpcclient
```

Ping the server
---------------

Send a JSON-RPC "ping" method to the server:

    >>> from jsonrpcclient.zmq_server import ZMQServer
    >>> ZMQServer('tcp://localhost:5000').request('ping')
    'pong'
