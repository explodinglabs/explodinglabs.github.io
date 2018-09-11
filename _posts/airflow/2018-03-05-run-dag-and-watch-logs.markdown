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
curl -O ~/airflow/plugins/log_config.py https://raw.githubusercontent.com/apache/incubator-airflow/master/airflow/config_templates/airflow_local_settings.py
```

Edit the file, changing `FILENAME_TEMPLATE` to this:
```sh
{% raw %}FILENAME_TEMPLATE = '{{ ti.dag_id }}/{{ ti.task_id }}.log'{% endraw %}
```

_Note:_ In the new Airflow 1.10, the "filename template" configuration setting
[has moved to the airflow.cfg
file](https://github.com/apache/incubator-airflow/blob/master/UPDATING.md#logging-configuration).

Set the logging_config_class in `airflow.cfg`:
```
logging_config_class = log_config.DEFAULT_LOGGING_CONFIG
```

Alternatively set the environment variable
`AIRFLOW__CORE__LOGGING_CONFIG_CLASS`.

## Tailing

Use [xtail](https://www.unicom.com/sw/xtail) to tail and follow files,
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
