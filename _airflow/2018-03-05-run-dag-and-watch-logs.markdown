---
layout: post
title: "Run an Airflow DAG from the command-line and watch the log output"
date: 2018-03-06
permalink: /airflow/run-dag-and-watch-logs
---
I prefer the command-line over web interfaces.

Here's how I run entire dags from start to finish, and watch the log output in
real-time in the terminal.

First start the Airflow scheduler.
```sh
$ airflow scheduler
```

Using `airflow run` or `airflow test` will run a single task and show you the
output, but to run a whole dag from start to finish, the command is `airflow
trigger_dag`. Unfortuntately, it doesn't show you any log output. The output
from tasks is sent to log files.

Each time any task is run, a new timestamped log file is created. Something
like
```
~/airflow/logs/my-dag/my-task/2018-03-06T09:59:10.427477
```

So we need to tail follow these files, new ones that appear. For this I use
[xtail](https://www.unicom.com/sw/xtail).

```sh
$ xtail ~/airflow/logs/my-dag/*
```

Now trigger the dag and watch the output.
```sh
$ airflow trigger_dag my-dag
```
