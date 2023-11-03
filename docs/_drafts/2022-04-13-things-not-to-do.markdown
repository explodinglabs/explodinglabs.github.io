---
layout: post
title: Don't do these things in Python
permalink: /things-to-avoid
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

<div id="intro" markdown="1">
As an industry we're transitioning away from imperative languages towards more
restricted, declarative, functional languages.
For now, if you have to use Python, here are some things to avoid.
</div>

## Logging

Unrestricted languages make it easy to add log entries all over the place, but
have some restraint.
If you log before and after every statement, now you have 3x the amount of
code, for not much benefit. The reader has to sift through all the logging
statements to see what the code is actually doing. (The first thing I do when
refactoring someone else's code is remove all the logging.)

Some logging is good, but be strategic about it. I suggest adding them late in
development, in a few key places.

## Exception handling (try blocks)


## Names prefixed with underscores

## Re-import into package files

## Implicitness

"Explicit is better than implicit" states the Zen of Python.

Defaults, fallbacks, implicit behaviour.

## None

## Logic branches that don't cover all cases

## State, mutation, iterations, classes
