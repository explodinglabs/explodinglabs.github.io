---
layout: post
category: python
date: 2016-08-06
title: "Sphinx Autodoc ImportError"
permalink: /sphinx-autodoc-importerror
---
<div class="wide-logos" markdown="1">
![airflow](/assets/python.png)
</div>

This drove me crazy today until I found the solution.

Sphinx autodoc was refusing to import any *new* modules added to the project.
Previously existing ones were importing fine.

The problem was a broken virtualenv. Recreated it and what do you know,
importing everything.
