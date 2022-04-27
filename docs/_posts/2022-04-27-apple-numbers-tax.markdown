---
layout: post
title: How to calculate Australian Personal Income Tax in Apple Numbers?
permalink: /apple-numbers-tax
---
Use this formula to calculate the income tax for an Employee or Sole Trader
in Australia as of 2022.
```
IF(A1≥180001,(A1−180000)×0.45+51667,
IF(A1≥120001,(A1−120000)×0.37+29467,
IF(A1≥45001,(A1−45000)×0.325+5092,
IF(A1≥18201,(A1−18200)×0.19,
0))))
```
