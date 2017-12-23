---
layout: post
title: "Sphinx Autodoc ImportError"
date: 2016-08-06
permalink: /sphinx-autodoc-importerror
---
This drove me crazy today until I found the solution.

Sphinx autodoc was refusing to import any *new* modules added to the project.
Previously existing ones were importing fine.

The problem was a broken virtualenv. Recreated it and what do you know,
importing everything.
