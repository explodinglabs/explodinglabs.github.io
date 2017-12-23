---
layout: post
title: "JSON-RPC in Python with jsonrpcserver"
date: 2016-08-05
permalink: /jsonrpc/jsonrpcserver
---
<div style="float: right" markdown="1">
![flask](/assets/flask.png)
</div>

We'll build an HTTP server in Python, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port 5000. It should respond to
"ping" with "pong".

Server
======

```sh
$ pip install jsonrpcserver
$ cat server.py
```
```python
from jsonrpcserver import Methods
methods = Methods()

@methods.add
def ping():
    return 'pong'

if __name__ == '__main__':
    methods.serve_forever()
```
```sh
$ python server.py
 * Listening on port 5000
```

Client
======

```sh
$ pip install jsonrpcclient requests
$ python
```
```python
>>> from jsonrpcclient.http_server import HTTPServer
>>> HTTPServer('http://localhost:5000/').request('ping')
'pong'
```
