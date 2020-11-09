---
layout: post
title: "Outlook for Mac: Search not finding emails"
permalink: /macos/outlook-search-not-finding-emails
---
Outlook for Mac wasn't finding all my emails when I searched.

The solution was to reindex spotlight.

As root:
```sh
mdutil -E /
```
