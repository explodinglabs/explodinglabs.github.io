---
layout: post
title: How to pipe jq to less, with colour?
permalink: /pipe-jq-to-less
---
Use `jq -C` to colorize the json, and `less -R` to output raw control
characters.

```sh
jq -C . data.json | less -R
```
