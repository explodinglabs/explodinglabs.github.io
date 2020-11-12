---
layout: post
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

I want to run dags and watch the log output in the terminal. Each time an
Airflow task is run, a new timestamped directory and file is created. Something
like:

```sh
~/airflow/logs/my-dag/my-task/2018-03-06T09:59:10.427477/1.log
```

This makes it hard to tail-follow the logs. Thankfully, starting from Airflow
1.9, logging can be configured easily, allowing you to put all of a dag's logs
into one file.

_Note 1:_ If you make this change, you won't be able to view task logs in the
web UI.

_Note 2:_ Logging to a single file is useful for development (using
SequentialExecutor), but it's **not recommended in production** because issues
will arise when multiple tasks attempt to write to the same log file at once.

## Easy Solution

_Requires Airflow 1.10+_

Set the `FILENAME_TEMPLATE` setting.

```sh
{% raw %}export AIRFLOW__CORE__LOG_FILENAME_TEMPLATE="{{ ti.dag_id }}.log"{% endraw %}
```

## Advanced Solution - Recommended

_Requires Airflow 1.9+_

Since Airflow 1.9, logging is configured pythonically.

Grab Airflow's default log config, `airflow_local_settings.py`, and copy it
somewhere in your `PYTHONPATH`.
```sh
curl -O https://raw.githubusercontent.com/apache/incubator-airflow/master/airflow/config_templates/airflow_local_settings.py
cp airflow_local_settings.py $AIRFLOW__CORE__DAGS_FOLDER
```

Set the logging_config_class setting. (Make sure this is set in both your
scheduler and worker's environments). (Alternatively set the related setting in
airflow.cfg.)
```sh
export AIRFLOW__CORE__LOGGING_CONFIG_CLASS=airflow_local_settings.DEFAULT_LOGGING_CONFIG
```

Now you can configure logging to your liking.

Edit airflow_local_settings.py, changing `FILENAME_TEMPLATE` to:
```sh
{% raw %}FILENAME_TEMPLATE = '{{ ti.dag_id }}.log'{% endraw %}
```

You should now get all of a dag log output in a single file.

## Tailing the logs

Start the scheduler and trigger a dag.
```sh
$ airflow scheduler
$ airflow trigger_dag my-dag
```

Watch the output with `tail -f`.

```sh
$ tail -f ~/airflow/logs/my-dag.log
```
