---
layout: post
category: python
date: 2016-08-04
title: "When to use Python's Decorators, Context Managers, Generators and Metaclasses"
permalink: /python/when-to-use
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

When to use Decorators
======================
- Add functionality before or after a method is executed.
- Data sanitization or addition.
- Function or class registration.
- Logging.

When to use Context Managers
============================
- Resource cleanliness (cleaning up after your code block).
- Handling exceptions, avoiding repetition.

When to use Generators
======================
- Accessing data in pieces.
- Computing data in pieces.

When to use Metaclasses
=======================
- Modify class structure from the way it was declared, (e.g. Django model).
- Class verification (ensure class conforms to a particular interface).
- Non-inheriting attributes. e.g. make an abstract class not inherit attributes.
- Class registration.

Some of this was taken from [Professional
Python](http://www.wrox.com/WileyCDA/WroxTitle/Professional-Python.productCd-1119070856.html)
by Luke Sneeringer.
