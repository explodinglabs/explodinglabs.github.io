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

We'll build an HTTP server in Python, taking JSON-RPC requests on port
5000. It should respond to "speak" with "meow". We'll use Python's built-in
http.server module, so no web framework is required. 

Server
======

Install dependencies
--------------------

```shell
$ pip install jsonrpcserver
```

Write server script
-------------------

Create a `server.py`:

```python
import logging
from http.server import BaseHTTPRequestHandler, HTTPServer
from jsonrpcserver import dispatch

def speak():
    return 'meow'

class TestHttpServer(BaseHTTPRequestHandler):

    def do_POST(self):
        # Process request
        request = self.rfile.read(int(self.headers['Content-Length'])).decode('utf-8')
        r = dispatch([speak], request)
        # Return response
        self.send_response(r.http_status)
        self.send_header('Content-type', 'application/json')
        self.end_headers()
        self.wfile.write(str(r).encode('utf-8'))

if __name__ == '__main__':
    logging.basicConfig(format='%(asctime)s %(message)s', level=logging.DEBUG)
    logging.debug('Listening on port %s', ADDRESS[1])
    HTTPServer(('localhost', 5000), TestHttpServer).serve_forever()
```

Start the server
----------------

```shell
$ python server.py
2016-08-01 14:57:07,061 Listening on port 5000
```

Client
======

Test with curl:

```shell
$ TYPE='Content-type: application/json'
$ MSG='{"jsonrpc": "2.0", "method": "speak", "id": 1}'
$ curl -H $TYPE -d $MSG http://localhost:5000
{"jsonrpc":"2.0","result":"meow","id":1}
```
