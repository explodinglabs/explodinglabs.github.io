---
layout: post
title: How to pipe jq to less, with colour?
permalink: /pipe-jq-to-less
---
Use `jq --color-output` to colorise the json,
combined with `less --RAW-CONTROL-CHARS` for ANSI colours to display .

```sh
jq --color-output . data.json | less --RAW-CONTROL-CHARS
```

Or shorthand:

```sh
jq -C . data.json | less -R
```

```
--color-output / -C

By default, jq outputs colored JSON if writing to a terminal.
You can force it to produce color even if writing to a pipe or a file using -C.
```
[jq Documentation](https://stedolan.github.io/jq/manual/#Invokingjq)

```
-R or --RAW-CONTROL-CHARS

Like -r, but only ANSI "color" escape sequences and OSC 8
hyperlink sequences are output in "raw" form.  Unlike -r,
the screen appearance is maintained correctly, provided
that there are no escape sequences in the file other than
these types of escape sequences.
```
[less documentation](https://man7.org/linux/man-pages/man1/less.1.html)
