---
layout: post
title: How to clear iMovie storage?
permalink: /clear-imovie-storage
---
The "Render files: Delete" button doesn't seem to work for me, so I use this command:
```sh
find ~/Movies/iMovie\ Library.imovielibrary -path "*/Render Files" -type d -exec rm -r {} +
```
It takes a while for the free space to appear in **Apple menu  > About This Mac > Storage**.
