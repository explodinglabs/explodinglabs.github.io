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
[JSON-RPC](http://www.jsonrpc.org/) requests on port 5000.  It should respond
to "speak" with "meow".

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
 * Restarting with stat
 * Debugger is active!
 * Debugger pin code: 216-262-392
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
>>> HTTPServer('http://localhost:5000/cat').request('speak')
'meow'
```
