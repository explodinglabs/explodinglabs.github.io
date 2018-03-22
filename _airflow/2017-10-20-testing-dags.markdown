---
layout: post
title: "Testing Airflow DAGs"
date: 2017-10-20
permalink: /airflow/testing-dags
redirect_from:
    - /airflow/testing-operators
    - /airflow/testing-airflow-operators
---
Developing Airflow dags involves writing unit tests for the individual tasks,
and then manually [running the whole dag from start to finish](/airflow/run-dag-and-watch-logs).

Here's a simple operator for testing:

```python
class MyOperator(BaseOperator):
    def execute(self, context):
        return 'foo'
```

Side note: Keep your operators light. Only put some controlling code in there.
The real work should be kept away from Airflow, in plain functions or classes.
Airflow is just a scheduler, don't do too much work in there.

Anyway, after testing those implementation functions, you should still test the
operator as well.

To test an operator's method in a unit test, you need to create three objects,
a dag, a task (the operator we're testing), and a TaskInstance. Here we test
`MyOperator.execute`.

```python
class TestMyOperator(TestCase):

    def test_execute(self):
        dag = DAG(dag_id='foo', start_date=datetime.now())
        task = MyOperator(dag=dag, task_id='foo')
        ti = TaskInstance(task=task, execution_date=datetime.now())
        result = task.execute(ti.get_template_context())
        self.assertEqual(result, 'foo')
```

If your operator is inside a _DAG definition file_, you should [hide the
globals section of that module](/airflow/hide-globals-in-dag-definition-file).
