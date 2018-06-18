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
>>> import jsonrpcclient
>>> jsonrpcclient.request("http://kodi:8080/jsonrpc", "Player.Open", item={"file": "plugin://plugin.video.youtube/?action=play_video&videoid=QwSazmPRfaI"})
--> {"jsonrpc": "2.0", "method": "Player.Open", "params": {"item": {"file": "plugin://plugin.video.youtube/?action=play_video&videoid=QwSazmPRfaI"}}, "id": 10}
<-- {"id":10,"jsonrpc":"2.0","result":"OK"} (200 OK)
'OK'
```

Change the `videoid` to your video.
