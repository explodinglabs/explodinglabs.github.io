---
layout: post
title: How to add Google Analytics to Readthedocs?
permalink: /rtd-analytics
---
To add your GA tracking ID to readthedocs:

1. Login to [readthedocs.org](https://readthedocs.org/), and browse to your project
3. Go to `Admin > Advanced Settings`
4. Enter the tracking ID into "Analytics code".

**If you use a custom theme**, you may need to add the code into `conf.py`. For
example, see `analytics_id` in Alabaster's [theme
options](http://alabaster.readthedocs.io/en/latest/customization.html#theme-options).
