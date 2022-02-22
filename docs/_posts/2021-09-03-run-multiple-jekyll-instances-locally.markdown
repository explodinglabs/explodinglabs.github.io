---
layout: post
title: Run multiple local Jekyll instances
permalink: /run-multiple-jekyll-instances-locally
---
If you're getting this error despite setting `--port` to an unused port:
```
no acceptor (port is in use or requires root privileges) (RuntimeError)
```

Set unused ports for both Jekyll and also LiveReload.
```sh
bundle exec jekyll serve --port 4001 --livereload --livereload-port 8001
```
