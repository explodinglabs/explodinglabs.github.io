---
layout: post
title: "SQL*Loader: Physical record longer than the maximum"
date: 2018-06-15
permalink: /oracle/sqlldr-physical-record-longer-than-maximum
redirects_from: /sqlldr/physical-record-longer-than-maximum
---
Was getting this error in sqlldr:
```
SQL*Loader-510: Physical record in data file (data.csv) is longer than the maximum(1048576)
```

Originally I attempted to set the `READSIZE` option, in the control file:
```
OPTIONS(READSIZE=10000000000)
```

However no value was large enough.

Eventually the problem was found to be a corrupted CSV file.
