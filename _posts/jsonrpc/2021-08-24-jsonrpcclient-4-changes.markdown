---
layout: post
category: jsonrpc
title: Changes in Jsonrpcclient 4
permalink: /jsonrpcclient-4-changes
---
<div class="warning">
    <p>Jsonrpcclient 4 requires Python 3.8+.</p>
</div>

Jsonrpcclient is a Python library that lets you generate JSON-RPC requests and
parse responses.

Version 4 is a complete rebuild.

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

- Relieves the burden of supporting the various protocols and frameworks.
- Gives the user control over how messages are sent and received.
- Instead of doing lots of things poorly, do a couple of things well.
- JSON-RPC is just a message format, so a JSON-RPC library should only deal with
  JSON-RPC messages, not the transport of them.

[Full version 4 documentation is
here](https://www.jsonrpcclient.com/en/latest/).
