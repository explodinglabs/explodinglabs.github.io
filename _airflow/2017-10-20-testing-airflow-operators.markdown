---
layout: post
title: "Testing Airflow Operators"
date: 2017-10-20
permalink: /airflow/testing-operators
redirect_from: /airflow/testing-airflow-operators
comments: true
---
It takes a few lines of setup before you can test an Airflow operator.

1. Instantiate a (fake) DAG.
2. Instantiate the operator we're testing.
3. Instantiate a TaskInstance.

Then you can test the method.

Here we test `MyOperator.execute` in Airflow 1.8:

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
            result = task.execute(ti.get_template_context())
            self.assertEqual(result, 'foo')
```

And in Airflow 1.7:

```python
class TestMyOperator(TestCase):
    def test_execute(self):
        dag = DAG(dag_id='foo')
        task = MyOperator(dag=dag, owner='foo', task_id='foo', start_date=datetime.now())
        ti = TaskInstance(task=task, execution_date=datetime.now())
        result = task.execute(ti.get_template_context())
        self.assertEqual(result, 1)
```
