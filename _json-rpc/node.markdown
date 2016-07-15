---
layout: page
title: "JSON-RPC over HTTP in Node"
permalink: /python/jsonrpc/node
---
{::options syntax_highlighter_opts="default_lang: javascript" /}

* TOC
{:toc}

Server
======

The server should handle incoming JSON-RPC requests on port 5555.

- When it receives a "speak" request on `/api/cats`, it should respond with "meow".
- When it receives a "speak" request on `/api/dogs`, it should respond with "woof".

Install requirements
--------------------

``` shell
$ npm install express jayson
```

Write server script
-------------------

Create a `server.js`:

    var express = require('express');
    var bodyParser = require('body-parser');
    var jayson = require('jayson');

    var cats = {
        speak: function(callback) {
            callback(null, 'meow');
        }
    }

    var dogs = {
        speak: function(callback) {
            callback(null, 'woof');
        }
    }

    var app = express();
    app.use(bodyParser.urlencoded({extended: true}));
    app.use(bodyParser.json());
    app.post('/api/cats', jayson.server(cats).middleware());
    app.post('/api/dogs', jayson.server(dogs).middleware());
    app.listen(5555);

Start the server
----------------

``` shell
$ node ./server.py
```

Client
======

Use curl to send requests:

```shell
$ TYPE='Content-type: application/json'
$ MSG='{"jsonrpc": "2.0", "method": "speak", "id": 1}'
$ curl -H $TYPE -d $MSG http://localhost:5555/api/cats
{"jsonrpc":"2.0","result":"meow","id":1}
$ curl -H $TYPE -d $MSG http://localhost:5555/api/dogs
{"jsonrpc":"2.0","result":"woof","id":1}
```
