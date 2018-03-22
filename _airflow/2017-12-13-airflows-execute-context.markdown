---
layout: post
date: 2017-12-13
title: Airflow's execute context
description:
    Showing the contents of the context dictionary, which is available in an
    Operator's execute method, or a PythonOperator's function definition.
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
    'dag': task.dag,
    'ds': ds,
    'ds_nodash': ds_nodash,
    'ts': ts,
    'ts_nodash': ts_nodash,
    'yesterday_ds': yesterday_ds,
    'yesterday_ds_nodash': yesterday_ds_nodash,
    'tomorrow_ds': tomorrow_ds,
    'tomorrow_ds_nodash': tomorrow_ds_nodash,
    'END_DATE': ds,
    'end_date': ds,
    'dag_run': dag_run,
    'run_id': run_id,
    'execution_date': self.execution_date,
    'latest_date': ds,
    'macros': macros,
    'params': params,
    'tables': tables,
    'task': task,
    'task_instance': self,
    'ti': self,
    'task_instance_key_str': ti_key_str,
    'conf': configuration,
    'test_mode': self.test_mode,
}
```

As a side note, you can generate the context from a TaskInstance object.

```python
ti = TaskInstance(task=task, execution_date=datetime.now())
task.execute(context=ti.get_template_context())
```
