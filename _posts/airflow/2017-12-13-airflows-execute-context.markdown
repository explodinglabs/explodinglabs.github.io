---
layout: post
date: 2017-12-13
title: Airflow's execute context
description:
    Showing the contents of the context dictionary, which is available in an
    Operator's execute method, or a PythonOperator's function definition.
category: airflow
image: /assets/airflow-wide.png
permalink: /airflow/execute-context
---
<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

I often forget the contents of the `context` dict, and it's not well
documented.

It can be found in `airflow/models.py`, in the
`TaskInstance.get_template_context` method.

```python
return {
    'END_DATE': ds,
    'conf': configuration,
    'dag': task.dag,
    'dag_run': dag_run,
    'ds': ds,
    'ds_nodash': ds_nodash,
    'end_date': ds,
    'execution_date': self.execution_date,
    'latest_date': ds,
    'macros': macros,
    'params': params,
    'run_id': run_id,
    'tables': tables,
    'task': task,
    'task_instance': self,
    'task_instance_key_str': ti_key_str,
    'test_mode': self.test_mode,
    'ti': self,
    'tomorrow_ds': tomorrow_ds,
    'tomorrow_ds_nodash': tomorrow_ds_nodash,
    'ts': ts,
    'ts_nodash': ts_nodash,
    'yesterday_ds': yesterday_ds,
    'yesterday_ds_nodash': yesterday_ds_nodash,
}
```

As a side note, you can generate the context from a TaskInstance object.

```python
ti = TaskInstance(task=task, execution_date=datetime.now())
task.execute(context=ti.get_template_context())
```
