---
layout: post
title: How to pipe jq to less, with colour?
permalink: /pipe-jq-to-less
---
Use `jq --color-output` to colorise the JSON,
combined with `less --RAW-CONTROL-CHARS` for ANSI colours to work.

```sh
jq --color-output . data.json | less --RAW-CONTROL-CHARS
```

Or shorthand:

```sh
jq -C . data.json | less -R
```

{% include google_in_article.html %}

From the [jq documentation](https://stedolan.github.io/jq/manual/#Invokingjq):
```
--color-output / -C

By default, jq outputs colored JSON if writing to a terminal.
You can force it to produce color even if writing to a pipe or a file using -C.
```

From the [less documentation](https://man7.org/linux/man-pages/man1/less.1.html):
```
-R or --RAW-CONTROL-CHARS

Like -r, but only ANSI "color" escape sequences and OSC 8
hyperlink sequences are output in "raw" form.  Unlike -r,
the screen appearance is maintained correctly, provided
that there are no escape sequences in the file other than
these types of escape sequences.
```
