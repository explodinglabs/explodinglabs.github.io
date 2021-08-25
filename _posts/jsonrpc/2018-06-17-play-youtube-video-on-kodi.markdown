---
layout: post
category: jsonrpc
title: Play a Youtube video on Kodi with JSON-RPC
permalink: /jsonrpc/kodi-youtube
---
<div class="warning">
    <p>This post is for Python 3.8+.</p>
</div>

<div class="wide-logos" markdown="1">
![kodi](/assets/kodi.png)
![json](/assets/json.png)
</div>

Play a Youtube video on Kodi, by sending a JSON-RPC request with Python.

```sh
pip install requests
pip install --pre jsonrpcclient
```

```python
import requests
from jsonrpcclient import request
params = {"file": "plugin://plugin.video.youtube/?action=play_video&videoid=QwSazmPRfaI"}
requests.post("http://kodi:8080/jsonrpc", json=request("Player.Open", params=params))
```

Change the `videoid` to your video.
