---
layout: post
title: "Testing Airflow operators"
date: 2017-10-20
permalink: /airflow/testing-operators
redirect_from: /airflow/testing-airflow-operators
---
It takes a few lines of setup before you can test an Airflow operator.

1. Instantiate a (fake) DAG.
2. Instantiate the operator we're testing.
3. Instantiate a TaskInstance.

Then you can test the method.

Here we test `MyOperator.execute` in Airflow 1.8:

```python
class TestMyOperator(TestCase):

    def test_execute(self):
        dag = DAG(dag_id='foo')
        task = MyOperator(dag=dag, task_id='foo', start_date=datetime.now())
        ti = TaskInstance(task=task, execution_date=datetime.now())
        result = task.execute(ti.get_template_context())
        self.assertEqual(result, 'foo')
```

(Airflow 1.7 also requires the `owner` passed to the task.)
