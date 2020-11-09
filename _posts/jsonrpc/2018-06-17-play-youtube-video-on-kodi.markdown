---
layout: post
category: jsonrpc
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
>>> from jsonrpcclient import request
>>> params = {"file": "plugin://plugin.video.youtube/?action=play_video&videoid=QwSazmPRfaI"}
>>> request("http://kodi:8080/jsonrpc", "Player.Open", item=params).data.result
'OK'
```

Change the `videoid` to your video.
