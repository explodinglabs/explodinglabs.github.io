---
layout: post
title: Clear iCloud Message Attachments
permalink: /clear-icloud-message-attachments
---
```sh
mkdir /Volumes/'Media 2021'/Messages/2023-11-02
cd ~/Library/Messages/Attachments
find . -type f | grep -v pluginPayloadAttachment | while read f; do echo $f; cp $f /Volumes/'Media 2021'/Messages/2023-11-02/; done`
```

Now go into System Settings > Beau Barker > iCloud > Account Storage: Manage > Messages.

Select all attachments and hit DEL.
