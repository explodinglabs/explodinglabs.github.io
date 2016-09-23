---
layout: post
title: "GraphQL in Python with ZeroMQ"
date: 2016-09-23
permalink: /graphql/zeromq
comments: true
---
<div class="wide-logos" markdown="1">
![ZeroMQ](/assets/zeromq.png)
![plus](/assets/plus.png)
![GraphQL](/assets/graphql.png)
</div>

We'll build a [ZeroMQ](http://zeromq.org/) server to take
[GraphQL](http://graphql.org/) queries.

Install the dependencies — [PyZMQ](https://pyzmq.readthedocs.io/) to take
queries and [Graphene](http://graphene-python.org/) to process them:

```sh
$ pip install pyzmq graphene
```
Create a `server.py`:

```python
import zmq
import graphene

class Query(graphene.ObjectType):
    hello = graphene.String(description='Hello')

    def resolve_hello(self, args, info):
        return 'World'

schema = graphene.Schema(query=Query)
socket = zmq.Context().socket(zmq.REP)

if __name__ == '__main__':
    socket.bind('tcp://*:5000')
    while True:
        request = socket.recv().decode()
        response = schema.execute(request)
        socket.send_string(str(response))
```
Start the server:

```sh
$ python server.py
```

Client
======
Test with pyzmq:

```python
>>> import zmq
>>> context = zmq.Context()
>>> socket = context.socket(zmq.REQ)
>>> socket.connect('tcp://localhost:5000')
>>> socket.send_string('{hello}')
>>> socket.recv().decode()
'{"data": {"hello": "World"}}'
```
