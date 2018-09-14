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
file is created with each run. Thankfully, starting from Airflow 1.9, logging
can be configured easily, allowing you to put all of a dag's logs into one
file.

_Note: If you make this change, you won't be able to view task logs in the web
UI, only in the terminal._

## Airflow 1.10 Solution

Set the `FILENAME_TEMPLATE` setting.

```sh
{% raw %}export AIRFLOW__CORE__LOG_FILENAME_TEMPLATE="{{ ti.dag_id }}.log"{% endraw %}
```

## Airflow 1.9 Solution

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

Edit airflow_local_settings.py, changing `FILENAME_TEMPLATE` to:
```sh
{% raw %}FILENAME_TEMPLATE = '{{ ti.dag_id }}.log'{% endraw %}
```

## Tailing the logs

Now you should get all of a task's log output in a single file.

Start the scheduler and trigger a dag.
```sh
$ airflow scheduler
$ airflow trigger_dag my-dag
```

Watch the output with `tail -f`.

```sh
$ tail -f ~/airflow/logs/my-dag.log
```
