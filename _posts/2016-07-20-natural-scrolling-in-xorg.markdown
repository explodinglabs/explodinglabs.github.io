---
layout: post
title: "Natural scrolling in Xorg"
date: 2016-07-20
permalink: /natural-scrolling-in-xorg
---

Edit `/etc/X11/xorg.conf.d/50-synaptics.conf`:

    Section "InputClass"
        ...
        Option "HorizScrollDelta" "-111"
        Option "VertScrollDelta" "-111"
    EndSection
