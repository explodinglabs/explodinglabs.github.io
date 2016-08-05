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

We'll build an HTTP server in Python, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port
5000. It should respond to 'ping' with 'pong'.

Server
======

``` shell
$ pip install werkzeug jsonrpcserver
$ cat server.py
```
```python
from werkzeug.wrappers import Request, Response
from werkzeug.serving import run_simple
from jsonrpcserver import dispatch

def ping():
    return 'pong'

@Request.application
def application(request):
    r = dispatch([ping], request.data.decode('utf-8'))
    return Response(str(r), r.http_status, mimetype='application/json')

if __name__ == '__main__':
    run_simple('localhost', 5000, application)
```
``` shell
$ python server.py
 * Running on http://localhost:5000/ (Press CTRL+C to quit)
```

Client
======

``` shell
$ pip install jsonrpcclient requests
$ python
```
```python
>>> from jsonrpcclient.http_server import HTTPServer
>>> HTTPServer('http://localhost:5000').request('ping')
'pong'
```
