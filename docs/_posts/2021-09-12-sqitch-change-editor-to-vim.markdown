---
layout: post
title: 'Sqitch: Change editor to Vim'
permalink: /sqitch/change-editor-to-vim
---
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
  from nano to `'vim --clean'`. (without `--clean` I got errors related to
  Python scripting).
- `docker build -t sqitch/sqitch --build-arg VERSION=1.1.0 .`
