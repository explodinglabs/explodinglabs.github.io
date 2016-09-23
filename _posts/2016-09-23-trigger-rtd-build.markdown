---
layout: post
title: "Trigger Readthedocs build from the commandline"
date: 2016-09-23
permalink: /trigger-rtd-build
comments: true
---
You can use curl to trigger a build:

```sh
$ curl -X POST https://readthedocs.org/build/myproject/latest
```

(Replace `myproject/latest` with your build info.)
