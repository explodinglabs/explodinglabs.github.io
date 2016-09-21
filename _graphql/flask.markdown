---
layout: post
title: "Graphql in Python with Flask"
date: 2016-09-21
permalink: /graphql/flask
comments: true
---
<div class="wide-logos" markdown="1">
![graphql](/assets/graphql.png)
![plus](/assets/plus.jpg)
![flask](/assets/flask.png)
</div>

We'll build a [Graphql](http://graphql.org/) server in Python, taking queries
on port 5000. It should respond to "ping" with "pong".

Install the dependencies —

- [Flask](http://flask.pocoo.org) will take queries,
- [graphene](http://graphene-python.org/) to process them, and
- [flask-graphql](https://github.com/graphql-python/flask-graphql) will simplify creating the route:

```shell
$ pip install flask graphene flask-graphql
```
Create a `server.py`:

```python
import graphene
from flask import Flask
from flask_graphql import GraphQLView

class Query(graphene.ObjectType):
    ping = graphene.String(description='Ping')
    def resolve_ping(self, args, context, info):
        return 'pong'

schema = graphene.Schema(query=Query)

app = Flask(__name__)
app.add_url_rule('/', view_func=GraphQLView.as_view('graphql', schema=schema))
app.run()
```

Start the server:

```shell
$ python server.py
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Client
======
Test with curl:

```shell
$ curl -H 'Content-type: application/graphql' -d '{ping}' http://localhost:5000
{"data":{"ping":"pong"}}
```
