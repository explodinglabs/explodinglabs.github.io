---
layout: post
title: Write 6x less code
permalink: /write-6x-less-code
redirect_from: /how-to-write-6x-less-code
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
```
_Followed by the same again ad infinitum._

## Logging before and after every f------ thing

_You don't need to log before doing everything._ "Get ready, here it comes!"
Who cares! Just do the thing!

_You don't need to log after doing everything._ "We succeeded, yay!" Who cares?

_You're only adding noise to the logs, and noise to the code._

## Trying to catch every f------ exception

This is the tendency of the paranoid programmer, every line of code brings
fear. "Something could go wrong here, I'd better handle it and log a nice
message. At least it'll show we foresaw the problem happening."

The interpreter will log the exception, so you don't need to do it yourself.

Maybe you're catching the exception to ignore it, this is usually a bad idea as
well.

There are untold number of exceptions that could occur. Just let them be. Stop
wrapping everything in little nets.

_You're only adding noise to the code._

## What's left after all the noise is removed

```python
do_something()
```

Worth adding: Logging and exceptions are side effects, so they come with all
the issues related to them; you lose referential transparency, more difficult
testability, etc. Use with care.
