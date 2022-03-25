---
layout: post
title: How to pipe jq to less, with colour?
permalink: /pipe-jq-to-less
---
Use `jq --color-output` to colorize the json,
and `less --raw-control-chars` for raw characters to be displayed.

```sh
jq --color-output . data.json | less --raw-control-chars
```

Or shorthand:
```sh
jq -C . data.json | less -R
```

> By default, jq outputs colored JSON if writing to a terminal.
> You can force it to produce color even if writing to a pipe or a file using -C.
