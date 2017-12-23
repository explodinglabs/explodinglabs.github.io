---
layout: post
title: "ImportError: cannot import name HTTPSHandler"
date: 2016-07-22
permalink: /importerror-httpshandler
---

Running tox tests tonight, had some failures on some Python 3.x versions:

    ImportError: cannot import name HTTPSHandler

Solution was to re-install those Python versions. In Arch:

    # packer -S python33 python34 python35
