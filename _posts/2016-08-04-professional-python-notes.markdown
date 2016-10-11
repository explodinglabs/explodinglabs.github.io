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

Notes from [*Professional Python*](https://www.amazon.com/gp/product/1119070856/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1119070856&linkCode=as2&tag=bcb0f-20&linkId=926e4032540c51b5c3e67637bc82420d) by Luke Sneeringer.
