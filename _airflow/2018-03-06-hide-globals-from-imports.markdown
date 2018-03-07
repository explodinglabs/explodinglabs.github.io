---
layout: post
title: "Hide globals when importing a DAG definition file"
date: 2018-03-06
permalink: /airflow/hide-globals-when-importing
---
Airflow has a fairly strange way of registering DAGs and tasks. They're put
into the global namespace of the DAG definition file.

```python
dag = DAG(dag_id='foo', start_date=start_date)
MyOperator(dag=dag, task_id='foo')
```

Airflow then comes along and finds them.

When importing that file however, as you do when unit testing, it's not ideal
to have those global objects to be created.

The solution is to protect that code by placing a predicate before it:

```python
if __name__ == 'unusual_prefix_my_module':
    dag = DAG(dag_id='foo', start_date=start_date)
    MyOperator(dag=dag, task_id='foo')
```

(Replace `my_module` with the name of the module.)

Airflow will still find your DAG as normal, however the code won't be executed
when the module is imported.
