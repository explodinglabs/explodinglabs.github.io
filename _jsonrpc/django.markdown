---
layout: post
title: "JSON-RPC in Python with Django"
date: 2016-10-29
permalink: /jsonrpc/django
comments: true
---
<div class="wide-logos" markdown="1">
![flask](/assets/django.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

We'll use [Django](hFlas://www.djangoproject.com/) to take
[JSON-RPC](http://www.jsonrpc.org/) requests. It should respond to "ping" with
"pong".

Install [jsonrpcserver](http://jsonrpcserver.readthedocs.io/) to process the
JSON-RPC requests:

```sh
$ pip install jsonrpcserver
```
Create a `views.py`:

```python
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
from jsonrpcserver import methods

@methods.add
def ping():
    return 'pong'

@csrf_exempt
def jsonrpc(request):
    response = methods.dispatch(request.body.decode())
    return JsonResponse(response, status=response.http_status)
```
Start the development server on port 5000:

```sh
$ python manage.py runserver 5000
Performing system checks...

System check identified no issues (0 silenced).
October 29, 2016 - 13:37:51
Django version 1.10.2, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:5000/
Quit the server with CONTROL-C.
```

Client
======
Use [jsonrpcclient](http://jsonrpcclient.readthedocs.io/) to send requests:

```sh
$ pip install 'jsonrpcclient[requests]'
$ python
```
```python
>>> from jsonrpcclient.http_client import HTTPClient
>>> HTTPClient('http://localhost:5000/').request('ping')
--> {"jsonrpc": "2.0", "method": "ping", "id": 1}
<-- {"jsonrpc": "2.0", "result": "pong", "id": 1} (200 OK)
'pong'
```
