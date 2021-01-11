---
layout: post
title: "How to write 7x more code than is necessary"
permalink: /how-to-write-7x-more-code-than-is-necessary
---
I see this repeatedly in my job as a software engineer (using impure imperative
languages):

```python
log("Doing something")
try:
    do_something()
    log("Did something")
except:
    log("There was an error")
    raise
```
_Followed by the same again ad infinitum._

## Logging before and after every f------ thing

_There's rarely any need to log before doing something._ "Get ready, here it
comes!" Who cares! Just do the thing!

_There's rarely any need to log after doing something._ "We succeeded, yay!"
Who cares?

_You're only adding noise to the logs, and noise to the code._

## Handling exceptions caused by every f------ thing

This is the tendency of the paranoid programmer -- every line of code they
write brings fear, "something could go wrong here, I'd better handle it and log
a nice message, at least it'll show we foresaw the problem happening!"

Maybe you're catching the exception to ignore it. This is usually a bad idea as
well.

Just let the exception occur.

_You're only adding noise to the code._

## What's left after all the noise is removed

```python
do_something()
```
