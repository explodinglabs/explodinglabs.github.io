---
layout: post
title: "JSON-RPC in Python with http.server"
date: 2016-08-01
permalink: /jsonrpc/httpserver
comments: true
---
<div style="float: right" markdown="1">
![python](/assets/python.png)
</div>

Server
======
We'll build an HTTP server in Python, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port
5000. It should respond to "ping" with "pong".

We'll use Python's built-in
[http.server](https://docs.python.org/3/library/http.server.html) module, so no
web framework is required - only
[jsonrpcserver](https://jsonrpcserver.readthedocs.io/en/latest/) to process the
messages.

```shell
$ pip install jsonrpcserver
```
Create a `server.py`:

```python
from http.server import BaseHTTPRequestHandler, HTTPServer
from jsonrpcserver import Methods, dispatch

methods = Methods()

@methods.add
def ping():
    return 'pong'

class TestHttpServer(BaseHTTPRequestHandler):
    def do_POST(self):
        # Process request
        request = self.rfile.read(int(self.headers['Content-Length'])).decode()
        r = dispatch(methods, request)
        # Return response
        self.send_response(r.http_status)
        self.send_header('Content-type', 'application/json')
        self.end_headers()
        self.wfile.write(str(r).encode())

if __name__ == '__main__':
    HTTPServer(('localhost', 5000), TestHttpServer).serve_forever()
```
Start the server:

```shell
$ python server.py
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
