---
layout: post
category: jsonrpc
title: JSON-RPC in Python with http.server
permalink: /jsonrpc/httpserver
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
![json](/assets/json.png)
</div>

We'll start a server to take [JSON-RPC](http://www.jsonrpc.org/) requests. It
should respond to "ping" with "pong".

We'll use Python's built-in
[http.server](https://docs.python.org/3/library/http.server.html) module, so no
web framework is required - only
[jsonrpcserver](https://www.jsonrpcserver.com/) to process the
messages:

```sh
$ pip install jsonrpcserver
```
Create a `server.py`:

```python
from http.server import BaseHTTPRequestHandler, HTTPServer

from jsonrpcserver import method, Result, Success, dispatch


@method
def ping() -> Result:
    return Success("pong")


class TestHttpServer(BaseHTTPRequestHandler):
    def do_POST(self):
        # Process request
        request = self.rfile.read(int(self.headers["Content-Length"])).decode()
        response = dispatch(request)
        # Return response
        self.send_response(200)
        self.send_header("Content-type", "application/json")
        self.end_headers()
        self.wfile.write(response.encode())


if __name__ == "__main__":
    HTTPServer(("localhost", 5000), TestHttpServer).serve_forever()
```

Start the server:

```sh
$ python server.py
```

## Client

Use [jsonrpcclient](https://www.jsonrpcclient.com/) to send requests:

``` shell
$ pip install "jsonrpcclient[requests]"
$ python
```
```python
>>> from jsonrpcclient import request
>>> request("http://localhost:5000", "ping").data.result
'pong'
```
