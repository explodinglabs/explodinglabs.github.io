---
layout: post
date: 2018-03-06
title: Hide globals in a DAG definition file
description:
    Don't instantiate the DAG and operators when importing your DAG definition
    file.
category: airflow
image: /assets/airflow-wide.png
permalink: /airflow/hide-globals-in-dag-definition-file
redirect_from: /airflow/hide-globals-when-importing
---
<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

Airflow has a fairly strange way of registering DAGs and tasks. They're put
into the global namespace of the DAG definition file.

```python
dag = DAG(dag_id='foo', start_date=start_date)
MyOperator(dag=dag, task_id='foo')
```

Airflow then comes along and finds them.

When importing that file however, as you do when unit testing, it's not ideal
to have those global objects created.

The solution is to protect that code by preceding it with a predicate:

```python
if __name__.startswith('unusual_prefix'):
    dag = DAG(dag_id='foo', start_date=start_date)
    MyOperator(dag=dag, task_id='foo')
```

Airflow will still find your DAG as normal, however that code won't be executed
when the module is imported.
