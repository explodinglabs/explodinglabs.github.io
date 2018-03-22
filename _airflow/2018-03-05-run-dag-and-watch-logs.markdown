---
layout: post
date: 2018-03-05
title: Run an Airflow DAG from the command-line and watch the log output
description:
    Explains how to run a DAG, completely from the command-line, and watch the
    log output in real-time.
image: /assets/airflow-wide.png
permalink: /airflow/run-dag-and-watch-logs
---
<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

I prefer the command-line over web interfaces.

Here's how I run entire dags from start to finish, and watch the log output in
real-time in the terminal.

First start the Airflow scheduler.

```sh
$ airflow scheduler
```

So now we need to trigger a dag, but unfortunately neither the `airflow
trigger_dag` command nor the scheduler shows log output from the tasks. The
output from tasks is sent to log files. Each time any task is run, a new
timestamped log file is created. Something like

```
~/airflow/logs/my-dag/my-task/2018-03-06T09:59:10.427477
```

To watch these files as they appear, I use
[xtail](https://www.unicom.com/sw/xtail).

```sh
$ xtail ~/airflow/logs/my-dag/*
```

(The directory and subdirectories may need to be created, if the dag hasn't
been run yet.)

Now trigger the dag and watch the output.
```sh
$ airflow trigger_dag my-dag
```
