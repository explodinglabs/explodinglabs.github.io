---
layout: post
category: micropython
title: First steps with Micropython on a NodeMCU
permalink: /micropython/first-steps
---
My NodeMCU arrived so I went right ahead and installed Micropython on it.

![nodemcu](/assets/nodemcu.png)

## Install the Micropython firmware

To copy the firmware onto the board, you can use *esptool*. It can be installed
with pip, so I created a virtualenv for installing it. Esptool requires Python
2.

```sh
$ mkvirtualenv -p $(which python2.7) esptool
```

Install esptool in the virtualenv:

```sh
$ pip install esptool
```

Plugging in the nodemcu gives me `/dev/ttyUSB0`.

Erase any existing firmware:

```sh
$ esptool.py --port /dev/ttyUSB0 erase_flash
```

Downloaded the [pre-built micropython
firmware](http://micropython.org/download/), then write the firmware to the
device:

```sh
$ esptool.py --port /dev/ttyUSB0 --baud 460800 write_flash --flash_size=8m -fm dio 0 esp8266-20160809-v1.8.3.bin
```

Now **replug the device** (or hit the **RST** button).

## Enter the REPL

I used picocom.

```sh
$ picocom -b115200 -ep /dev/ttyUSB0
```
```sh
picocom v2.1

port is        : /dev/ttyUSB0
flowcontrol    : none
baudrate is    : 115200
parity is      : none
databits are   : 8
stopbits are   : 1
escape is      : C-p
local echo is  : no
noinit is      : no
noreset is     : no
nolock is      : no
send_cmd is    : sz -vv
receive_cmd is : rz -vv -E
imap is        :
omap is        :
emap is        : crcrlf,delbs,

Type [C-p] [C-h] to see available commands

Terminal ready
```

Press enter to see the prompt:

```sh
>>>
```

## Notes

- **Specify the baudrate** of 115200. Without this it said *Terminal Ready*,
but there was no prompt and I couldn't communicate at all. Once I specified the
baudrate with the `-b` option, the prompt appears (after pressing enter).

- I changed picocom's escape command to `C-p` with the `-e` option, because
`C-a` clashed with my tmux setup.

- To exit use `[C-p]`, ``C-\``, `[C-p]`, `C-x`.

## Now see

[How to copy files to a Micropython device](https://beau.click/micropython/mipy)
