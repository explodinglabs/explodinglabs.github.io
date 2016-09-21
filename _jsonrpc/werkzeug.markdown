---
layout: post
title: "JSON-RPC in Python with Werkzeug"
date: 2016-08-01
permalink: /jsonrpc/werkzeug
comments: true
---
<div style="float: right" markdown="1">
![werkzeug](/assets/werkzeug.png)
</div>

Server
======
We'll build an HTTP server in Python, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port
5000. It should respond to 'ping' with 'pong'.

Install the dependencies — [Werkzeug](http://werkzeug.pocoo.org) to take
requests and [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process
them:

``` shell
$ pip install werkzeug jsonrpcserver
```
Create a `server.py`:

```python
from werkzeug.wrappers import Request, Response
from werkzeug.serving import run_simple
from jsonrpcserver import Methods, dispatch

methods = Methods()

@methods.add
def ping():
    return 'pong'

@Request.application
def application(request):
    r = dispatch(methods, request.data.decode())
    return Response(str(r), r.http_status, mimetype='application/json')

run_simple('localhost', 5000, application)
```
Start the server:

``` shell
$ python server.py
 * Running on http://localhost:5000/ (Press CTRL+C to quit)
```

Client
======
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

``` shell
$ pip install 'jsonrpcclient[requests]'
$ python
```
```python
>>> from jsonrpcclient.http_client import HTTPClient
>>> HTTPClient('http://localhost:5000').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```
