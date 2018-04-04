---
layout: post
category: python
date: 2016-07-22
title: "ImportError: cannot import name HTTPSHandler"
permalink: /importerror-httpshandler
---
<div class="wide-logos" markdown="1">
![airflow](/assets/python.png)
</div>

Running tox tests tonight, had some failures on some Python 3.x versions:

    ImportError: cannot import name HTTPSHandler

Solution was to re-install those Python versions. In Arch:

    # packer -S python33 python34 python35
