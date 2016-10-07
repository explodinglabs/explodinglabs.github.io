---
layout: post
title: "JSON-RPC in Python with Werkzeug"
date: 2016-08-01
permalink: /jsonrpc/werkzeug
comments: true
---
<div class="wide-logos" markdown="1">
![werkzeug](/assets/werkzeug.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll use [Werkzeug](http://werkzeug.pocoo.org) to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to 'ping' with
'pong'.

Install Werkzeug to take requests and
[jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process them:

``` shell
$ pip install werkzeug jsonrpcserver
```
Create a `server.py`:

```python
from werkzeug.wrappers import Request, Response
from werkzeug.serving import run_simple
from jsonrpcserver import methods

@methods.add
def ping():
    return 'pong'

@Request.application
def application(request):
    r = methods.dispatch(request.data.decode())
    return Response(str(r), r.http_status, mimetype='application/json')

if __name__ == '__main__':
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
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1} (200 OK)
'pong'
```
