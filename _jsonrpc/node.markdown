---
layout: post
title: "JSON-RPC in Node with Express"
date: 2016-08-01
permalink: /jsonrpc/node
comments: true
---
<div style="float: right" markdown="1">
![nodejs](/assets/nodejs.png)
</div>

We'll build an HTTP server in Node, taking [JSON-RPC](http://www.jsonrpc.org/) requests on port 5000.

- When it receives a "speak" request on `/cats`, it should respond with "meow".
- When it receives a "speak" request on `/dogs`, it should respond with "woof".

Server
======

``` shell
$ npm install express body-parser jayson
$ cat server.js
```
```javascript
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
app.post('/cats', jayson.server(cats).middleware());
app.post('/dogs', jayson.server(dogs).middleware());
app.listen(5000);
```
``` shell
$ node server.js
```

Client
======

Use curl to send requests:

```shell
$ HDR='Content-type: application/json'
$ MSG='{"jsonrpc": "2.0", "method": "speak", "id": 1}'
$ curl -H $HDR -d $MSG http://localhost:5000/cats
{"jsonrpc":"2.0","result":"meow","id":1}
$ curl -H $HDR -d $MSG http://localhost:5000/dogs
{"jsonrpc":"2.0","result":"woof","id":1}
```
