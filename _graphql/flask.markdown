---
layout: post
title: "GraphQL in Python with Flask"
date: 2016-09-21
permalink: /graphql/flask
comments: true
---
<div class="wide-logos" markdown="1">
![Flask](/assets/flask.png)
![plus](/assets/plus.png)
![GraphQL](/assets/graphql.png)
</div>

We'll build a [Flask](http://flask.pocoo.org/) server to take
[GraphQL](http://graphql.org/) queries.

Install the dependencies — Flask to take queries,
[Graphene](http://graphene-python.org/) to process them and
[Flask-GraphQL](https://github.com/graphql-python/flask-graphql) to simplify
the route:

```sh
$ pip install flask graphene flask-graphql
```
Create a `server.py`:

```python
from flask import Flask
from graphene import ObjectType, String, Schema
from flask_graphql import GraphQLView

class Query(ObjectType):
    hello = String(description='Hello')
    def resolve_hello(self, args, context, info):
        return 'World'

view_func = GraphQLView.as_view('graphql', schema=Schema(query=Query))

app = Flask(__name__)
app.add_url_rule('/', view_func=view_func)

if __name__ == '__main__':
    app.run()
```
Start the server:

```sh
$ python server.py
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

## Client

Test with curl:

```sh
$ curl -g 'http://localhost:5000/?query={hello}'
{"data":{"hello":"World"}}
```

## Python Client

```sh
$ pip install gql requests
```
```python
import json
from gql import gql, Client
from gql.transport.requests import RequestsHTTPTransport

transport = RequestsHTTPTransport('http://localhost:5000/')
client = Client(transport=transport)
response = client.execute(gql('{hello}'))

json.dumps(response)
```
```python
>>>
{"hello": "World"}
```
