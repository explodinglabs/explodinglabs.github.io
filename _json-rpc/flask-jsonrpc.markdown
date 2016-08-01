---
layout: post
title: "JSON-RPC in Python with Flask"
date: 2016-08-01
permalink: /python/flask/jsonrpc
comments: true
---
<div style="float: right" markdown="1">
![flask](/assets/flask.png)
</div>

We'll build an HTTP server in Python. It should take JSON-RPC requests on port
5000, responding to "speak" with "meow".

* TOC
{:toc}

Server
======

Install dependencies
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

def speak():
    return 'meow'

@app.route('/cat', methods=['POST'])
def index():
    r = dispatch([speak], request.get_data().decode('utf-8'))
    return Response(str(r), r.http_status, mimetype='application/json')

if __name__ == '__main__':
    app.run()
```

Start the server
----------------

```shell
$ python server.py
```

Client
======

Install dependencies
--------------------

```shell
$ pip install requests jsonrpcclient
```

Send request
------------

Send a JSON-RPC "speak" request:

```python
>>> from jsonrpcclient.http_server import HTTPServer
>>> s = HTTPServer('http://localhost:5000/cat')
>>> s.request('speak')
'meow'
```
