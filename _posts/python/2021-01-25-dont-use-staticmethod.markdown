---
layout: post
category: python
title: Don't use @staticmethod
permalink: /python/dont-use-staticmethod
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

In Python, don't use the `@staticmethod` decorator.

A static method is just a function, it doesn't need to be inside a class. So
move it out, Write a plain function instead.
