---
layout: post
title: How to test your readthedocs documentation locally?
permalink: /build-readthedocs-locally
---
Install [Sphinx](https://www.sphinx-doc.org/en/master/usage/installation.html).
```sh
pip install sphinx
pip install -r requirements-docs.txt  # theme and code highlighter
```

Build your docs:
```sh
$ sphinx-build -a doc /tmp/mydocs
```

Open the html file in your browser, for example:
```
file:///tmp/jsonrpcserver/index.html
```
