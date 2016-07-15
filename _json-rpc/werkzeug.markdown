---
layout: page
title: "JSON-RPC over HTTP in Werkzeug"
permalink: /python/werkzeug/jsonrpc
---
{::options syntax_highlighter_opts="default_lang: python" /}

<div style="float: right" markdown="1">
![werkzeug](/assets/werkzeug.png)
</div>

* TOC
{:toc}

Server
======

The server should handle incoming JSON-RPC requests on port 5000.

Install requirements
--------------------

``` shell
$ pip install werkzeug jsonrpcserver
```

Write server script
-------------------

Create a `server.py`:

    from werkzeug.wrappers import Request, Response
    from werkzeug.serving import run_simple
    from jsonrpcserver import dispatch

    def square(x):
        return x * x

    def cube(x):
        return x * x * x

    @Request.application
    def application(request):
        r = dispatch([square, cube], request.data.decode('utf-8'))
        return Response(str(r), r.http_status, mimetype='application/json')

    if __name__ == '__main__':
        run_simple('localhost', 5000, application)

Start the server
----------------

``` shell
$ python server.py
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
    >>> s = ZMQServer('tcp://localhost:5000')
    >>> s.request('square', 3)
    9
    >>> s.request('cube', 3)
    27
