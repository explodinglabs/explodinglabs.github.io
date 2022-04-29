---
layout: post
title: How to trigger a Readthedocs build from the commandline?
permalink: /trigger-rtd-build
---
You can use curl to trigger a build:

```sh
curl -X POST https://readthedocs.org/build/myproject/latest
```

(Replace `myproject/latest` with your project name and version.)
