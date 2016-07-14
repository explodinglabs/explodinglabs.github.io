---
layout: post
title: "Send and receive JSON-RPC over ZeroMQ in Python"
date: 2016-07-14 00:54:00 +10:00
categories: python zeromq json-rpc
---
{::options syntax_highlighter_opts="default_lang: python" /}

Server
======

Handle incoming JSON-RPC requests on port 5555:

``` shell
$ pip install pyzmq jsonrpcserver
$ vim server.py
```

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

Save and run the script to start the server:

``` shell
$ python ./server.py
```

Client
======

Send a JSON-RPC "ping" method to the server:

``` shell
$ pip install pyzmq jsonrpcclient
$ python
```

    >>> from jsonrpcclient.zmq_server import ZMQServer
    >>> ZMQServer('tcp://localhost:5555').request('ping')
    'pong'
