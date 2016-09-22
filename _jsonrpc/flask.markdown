---
layout: post
title: "JSON-RPC in Python with Flask"
date: 2016-08-01
permalink: /jsonrpc/flask
comments: true
---
<div class="wide-logos" markdown="1">
![flask](/assets/flask.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll build a [Flask](http://flask.pocoo.org) server to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install the dependencies — Flask to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

```shell
$ pip install flask jsonrpcserver
```
Create a `server.py`:

```python
from flask import Flask, request, Response
from jsonrpcserver import Methods, dispatch

app = Flask(__name__)
methods = Methods()

@methods.add
def ping():
    return 'pong'

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
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1} (200 OK)
'pong'
```
