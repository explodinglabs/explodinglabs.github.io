---
layout: post
title: "Pipe jq to less, with colour"
permalink: /pipe-jq-to-less
---

Use `jq -C` and `less -R`.

```sh
$ jq -C . data.json |less -R
```
