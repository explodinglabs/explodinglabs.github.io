---
layout: post
title: "JSON-RPC in Python with Flask"
date: 2016-08-01
permalink: /jsonrpc/flask
comments: true
---
<div style="float: right" markdown="1">
![flask](/assets/flask.png)
</div>

We'll build an HTTP server in Python, taking
[JSON-RPC](http://www.jsonrpc.org/) requests on port 5000. It should respond to
"ping" with "pong".

Install the dependencies — [Flask](http://flask.pocoo.org) to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```shell
$ pip install flask jsonrpcserver
```
Create a `server.py`:

```python
from flask import Flask, request, Response
from jsonrpcserver import Methods, dispatch

methods = Methods()
@methods.add
def ping():
    return 'pong'

app = Flask(__name__)
@app.route('/', methods=['POST'])
def index():
    r = dispatch(methods, request.get_data().decode())
    return Response(str(r), r.http_status, mimetype='application/json')

if __name__ == '__main__':
    app.run()
```
Start the server:

```shell
$ python server.py
 * Restarting with stat
 * Debugger is active!
 * Debugger pin code: 216-262-392
```

Client
======
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

```shell
$ pip install 'jsonrpcclient[requests]'
$ python
```
```python
>>> from jsonrpcclient.http_client import HTTPClient
>>> HTTPClient('http://localhost:5000/').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1}
'pong'
```
