---
layout: post
date: 2018-03-05
title: Run an Airflow DAG from the command-line and watch the log output
description:
    Explains how to run a DAG, completely from the command-line, and watch the
    log output in real-time.
category: airflow
image: /assets/airflow-wide.png
permalink: /airflow/run-dag-and-watch-logs
---
<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

I prefer the command-line over web interfaces.

I want to run dags and watch the log output in the terminal.

Output from tasks is sent to log files. Each time a task is run, a new
timestamped directory and log file is created. Something like:

```sh
~/airflow/logs/my-dag/my-task/2018-03-06T09:59:10.427477/1.log
```

This makes it hard to tail and follow the logs, because a new directory and
file is created with each run.

## Solution

Thankfully, starting from Airflow 1.9, logging can be configured easily.

Copy Airflow's log config template file to somewhere in your `PYTHONPATH`.
```sh
curl -O https://raw.githubusercontent.com/apache/incubator-airflow/master/airflow/config_templates/airflow_local_settings.py
```

Set the environment variable `AIRFLOW__CORE__LOGGING_CONFIG_CLASS`. (Make sure
this is set in your scheduler and worker's environments).
```sh
export AIRFLOW__CORE__LOGGING_CONFIG_CLASS=airflow_local_settings.DEFAULT_LOGGING_CONFIG
```

Now you can configure the logging to your liking in the airflow_local_settings
module.

I like to put all of a task's logs into one file. For this, set the
`FILENAME_TEMPLATE` setting.

_Note: If you make this change, you won't be able to view task logs in the web
UI, only in the terminal._

In Airflow 1.10, set the following environment variable.
```sh
{% raw %}export AIRFLOW__CORE__LOG_FILENAME_TEMPLATE="{{ ti.dag_id }}/{{ ti.task_id }}.log"{% endraw %}
```

In Airflow 1.9, edit airflow_local_settings.py, changing `FILENAME_TEMPLATE` to:
```sh
{% raw %}FILENAME_TEMPLATE = '{{ ti.dag_id }}/{{ ti.task_id }}.log'{% endraw %}
```

Now you should get all of a task's log output in a single file, and can tail
the file.

```
tail -f ~/airflow/logs/my-dag/my-task.log
```

## Better Tailing

I use [xtail](https://www.unicom.com/sw/xtail) to tail and follow files,
including newly created ones.

```sh
xtail ~/airflow/logs/my-dag
```

Now start the scheduler and trigger a dag.
```sh
$ airflow scheduler
$ airflow trigger_dag my-dag
```

Watch the output in xtail.
