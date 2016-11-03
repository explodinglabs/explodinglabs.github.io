---
layout: post
title: "Pipe jq to less, with colour"
date: 2016-11-03
permalink: /pipe-jq-to-less
comments: false
---

Use `jq -C` and `less -R`.

```sh
$ jq -C . data.json |less -R
```
