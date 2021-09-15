---
layout: post
title: Clear iMovie storage
permalink: /clear-imovie-storage
---
The Render files: Delete button in preferences doesn't seem to do it for me, so I use:
```sh
find ~/Movies/iMovie\ Library.imovielibrary -path "*/Render Files" -type d -exec rm -r {} +
```
It takes a while for the free space to appear in Apple menu  > About This Mac > Storage.
