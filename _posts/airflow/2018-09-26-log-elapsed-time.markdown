---
layout: post
date: 2018-09-26
title: Log elapsed time
description: How to get the elapsed time since the dag run began, or another task began, and log it.
category: airflow
permalink: /airflow/log-elapsed-time
---
Log the elapsed time since another task began:

```python
class CompletedOperator(BaseOperator):
    def __init__(self, other_task_id: str):
        self.other_task_id = other_task_id

    def execute(self, context):
        self.log.info(
            "Process completed succesfully in %s",
            str(
                datetime.now(timezone.utc)
                - context["dag_run"].get_task_instance(self.other_task_id).execution_date
            ),
        )
```

```
Process completed successfully in 0:02:10.823002
```
