---
layout: post
category: jsonrpc
title: What are the changes in Jsonrpcclient 4?
permalink: /jsonrpcclient-4-changes
---
Jsonrpcclient is a Python library that creates JSON-RPC requests for sending,
and parses responses. Version 4 is a complete rebuild.

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/PxQagaZ0PsY" frameborder="0" allowfullscreen></iframe>
</div>

## Simpler feature set

The new version is more lightweight and gives the user more control.

The previous version did too much:

1. Generate a request
2. Send the request
3. Receive the response
4. Parse the response

The new version still helps you generate a request, but doesn't send it or
receive the response. This is left to the user. Once you've received a
response, the library will help you parse it.

1. **Generate a request**
2. <del>Send the request</del> -- Now left to the user
3. <del>Receive the response</del> -- Now left to the user
4. **Parse the response**

## Why remove the transport from the library?

- Gives the user control over how messages are sent and received.
- Support every protocol, not just a few. 
- JSON-RPC is just a message format, so a JSON-RPC library should only deal with
  JSON-RPC messages, not the transport of them.
- Relieves the burden of supporting the various protocols and frameworks.
- Instead of doing lots of things poorly, do a couple of things well.

## Usage comparison

Previously (using [requests](https://docs.python-requests.org/en/master/)):
```python
from jsonrpcclient.clients.http_client import HTTPClient

client = HTTPClient("http://localhost:5000")
response = client.request("ping")
print(response.data.result)
```

Now:
```python
from jsonrpcclient import parse, request
import requests

response = requests.post("http://localhost:5000/", json=request("ping"))
parsed = parse(response.json())
print(parsed.result)
```

Keep in mind the response may be an error, so in production code you should do
runtime type checking on the parsed value, or in Python 3.10+, use pattern
matching.

[See examples in various
frameworks.](https://github.com/explodinglabs/jsonrpcclient/tree/master/examples)

[Full version 4 documentation is
here.](https://www.jsonrpcclient.com/en/latest/)
