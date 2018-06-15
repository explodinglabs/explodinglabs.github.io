---
layout: post
title: "SQL*Loader: Physical record longer than the maximum"
date: 2018-06-15
permalink: /sqlldr/physical-record-longer-than-maximum
---
Was getting this error in sqlldr:
```
SQL*Loader-510: Physical record in data file (incoming/TODS/FFL/data.csv) is longer than the maximum(1048576)
```

Solution is to set the `readsize` option, in the command:
```
sqlldr readsize=10000000000 ...
```

Or in the control file:
```
OPTIONS(READSIZE=10000000000)
```
