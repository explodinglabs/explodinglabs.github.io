---
layout: post
title: "Airflow's execute context"
date: 2017-12-13
permalink: /airflow/execute-context
comments: false
---
The contents of this dict can be found in the `get_template_context` method of
`models.py`.

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
