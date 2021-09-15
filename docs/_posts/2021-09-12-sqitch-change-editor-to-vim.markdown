---
layout: post
title: 'Sqitch: Change editor to Vim'
permalink: /sqitch/change-editor-to-vim
---
An editor is only used by Sqitch for certain things such as entering a note for
a new migration, but if you use `sqitch add` with the `--note` (or `-n`) param
it's not really necessary to change this unless you really want to.

## How to change the editor

If you installed Sqitch (instead of using the docker image), the easiest way is
to create/edit the config file (such as `~/.sqitch/sqitch.conf`):
```ini
[core]
    editor = vim
```

If like me you use the docker image `sqitch/sqitch` from docker hub,
unfortunately it doesn't include vim in the container. So I had to:

- Fork the [docker-sqitch repository](https://github.com/sqitchers/docker-sqitch).
- Edit the Dockerfile to replace `nano` with `vim`. Also change SQITCH_EDITOR
  from nano to `'vim --clean'`. (without `--clean` I had errors related to
  Python scripting).
- `docker build -t sqitch/sqitch --build-arg VERSION=1.1.0 .`
