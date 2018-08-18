---
layout: post
category: jsonrpc
date: 2018-06-17
title: Play a Youtube video on Kodi with JSON-RPC
permalink: /jsonrpc/kodi-youtube
---
<div class="wide-logos" markdown="1">
![kodi](/assets/kodi.png)
![plus](/assets/plus.png)
![json](/assets/json.png)
</div>

Play a Youtube video on Kodi, by sending a JSON-RPC request with Python.

```sh
pip install "jsonrpcclient[requests]"
```

```python
>>> from jsonrpcclient.clients.http_client import HTTPClient
>>> params = {"file": "plugin://plugin.video.youtube/?action=play_video&videoid=QwSazmPRfaI"}
>>> HTTPClient("http://kodi:8080/jsonrpc").request("Player.Open", item=params).data.result
'OK'
```

Change the `videoid` to your video.
