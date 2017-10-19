---
layout: post
title: "Testing Airflow Operators"
date: 2017-10-16
permalink: /airflow/testing-airflow-operators
comments: true
---
Create a simple operator in `my_operator.py`:
```python
from airflow.models import BaseOperator

class MyOperator(BaseOperator):
    def execute(self, context):
        return 'foo'
```

Now test it:
```python
from unittest import TestCase
from datetime import datetime
from airflow.models import DAG, TaskInstance
from my_operator import MyOperator

class TestMyOperator(TestCase):
    def test_execute(self):
        with DAG(dag_id='foo'):
            task = MyOperator(task_id='foo', start_date=datetime.now())
            ti = TaskInstance(task=task, execution_date=datetime.now())
            result = task.execute({'ti': ti, 'task': task})
            self.assertEqual(result, 'foo')
```
