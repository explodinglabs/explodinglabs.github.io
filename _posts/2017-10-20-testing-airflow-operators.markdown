---
layout: post
title: "Testing Airflow Operators"
date: 2017-10-20
permalink: /airflow/testing-airflow-operators
comments: true
---
Create a simple operator to test in `my_operator.py`:
```python
from airflow.models import BaseOperator

class MyOperator(BaseOperator):
    def execute(self, context):
        return 'foo'
```

Now test it in a `test_my_operator.py`:
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
            result = task.execute(context={'ti': ti, 'task': task})
            self.assertEqual(result, 'foo')
```

Run the test:
```
$ python -m unittest test_my_operator -v
[2017-10-20 10:50:34,722] {__init__.py:57} INFO - Using executor SequentialExecutor
test_execute (test_my_operator.TestMyOperator) ... ok

----------------------------------------------------------------------
Ran 1 test in 0.088s

OK
```
