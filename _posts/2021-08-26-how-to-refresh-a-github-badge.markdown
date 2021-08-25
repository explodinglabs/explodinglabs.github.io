---
layout: post
title: How to refresh a Github badge
permalink: /refresh-github-badge
---
This is an issue with Github's cache.

Grab the badge URL and purge it:
```sh
$ curl -X PURGE https://camo.githubusercontent.com/599a541f117b37b0d66284bd3103856d2d484d4714945381697bc9c242b3025d/68747470733a2f2f636f766572616c6c732e696f2f7265706f732f6769746875622f6578706c6f64696e676c6162732f6a736f6e727063636c69656e742f62616467652e7376673f6272616e63683d6d6173746579
{ "status": "ok", "id": "11253-1628767133-733" }
```
