---
layout: page
title: "JSON-RPC in Python with Flask"
permalink: /python/flask/jsonrpc
---
<div style="float: right" markdown="1">
![flask](/assets/flask.png)
</div>

* TOC
{:toc}

Server
======

The server should handle incoming JSON-RPC requests on port 5000.

Install requirements
--------------------

```shell
$ pip install flask jsonrpcserver
```

Write server script
-------------------

Create a `server.py`:

```python
from flask import Flask, request, Response
from jsonrpcserver import dispatch

app = Flask(__name__)

def square(x):
    return x * x

def cube(x):
    return x * x * x

@app.route('/api', methods=['POST'])
def index():
    r = dispatch([square, cube], request.get_data().decode('utf-8'))
    return Response(str(r), r.http_status, mimetype='application/json')

if __name__ == '__main__':
    app.run(debug=True)
```

Start the server
----------------

```shell
$ python server.py
```

Client
======

Install requirements
--------------------

```shell
$ pip install requests jsonrpcclient
```

Call the methods
-------------

Send JSON-RPC "square" and "cube" requests:

```python
>>> from jsonrpcclient.http_server import HTTPServer
>>> s = HTTPServer('http://localhost:5000/api')
>>> s.request('square', 3)
9
>>> s.request('cube', 3)
27
```
