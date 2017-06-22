---
layout: post
title: "When to use Decorators, Context-Managers, Generators and Metaclasses"
date: 2016-08-04
permalink: /python/when-to-use
comments: true
---
When to use Decorators
======================
- Add functionality before or after a method is executed
- Data sanitization or addition
- Function registration

When to use Context-Managers
============================
- Resource cleanliness (cleaning up after your code block)
- Handling exceptions, avoiding repetition

When to use Generators
======================
- Accessing data in pieces
- Computing data in pieces

When to use Metaclasses
=======================
- Modify class structure from the way it was declared, (e.g. Django model)
- Class verification (ensure class conforms to a particular interface)
- Non-inheriting attributes. e.g. make an abstract class not inherit attributes

These notes are from [Professional
Python](http://www.wrox.com/WileyCDA/WroxTitle/Professional-Python.productCd-1119070856.html)
by Luke Sneeringer.
