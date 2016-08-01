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
