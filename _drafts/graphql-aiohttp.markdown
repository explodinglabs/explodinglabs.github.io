---
layout: post
title: "GraphQL in Python with aiohttp"
date: 2016-09-23
permalink: /graphql/aiohttp
comments: true
---
<div class="wide-logos" markdown="1">
![aiohttp](/assets/aiohttp.png)
![plus](/assets/plus.png)
![GraphQL](/assets/graphql.png)
</div>

We'll build an [aiohttp](http://aiohttp.readthedocs.io/) server, taking
[GraphQL](http://graphql.org/) queries and processing them asynchronously.

Install the dependencies —

- [aiohttp](http://aiohttp.readthedocs.io/) to take queries, and
- [Graphene](http://graphene-python.org/) to process them.

```shell
$ pip install aiohttp graphene
```
Create a `server.py`:

```python
from aiohttp import web
from graphene import ObjectType, String, Schema

class Query(ObjectType):
    hello = String(description='Hello')
    def resolve_hello(self, args, info):
        return 'World'

schema = Schema(query=Query)

async def graphql(query):
    return schema.execute(query)

async def handle(request):
    query = await request.text()
    result = await graphql(query)
    return web.json_response(result.response)

app = web.Application()
app.router.add_post('/', handle)

if __name__ == '__main__':
    web.run_app(app, port=5000)
```
Start the server:

```shell
$ python server.py
======== Running on http://0.0.0.0:5000/ ========
(Press CTRL+C to quit)
```

Client
======
Test with curl:

```shell
curl -H 'Content-type: application/graphql' -d '{hello}' http://localhost:5000
{"data": {"hello": "World"}}% 
```
