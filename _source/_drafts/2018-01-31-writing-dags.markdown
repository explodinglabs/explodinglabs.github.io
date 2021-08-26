---
layout: post
date: 2018-01-31
title: How to write an Airflow DAG
description: Tips on writing DAGs.
category: airflow
image: /assets/airflow-wide.png
permalink: /airflow/tips
---
<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

To add:
- Don't share a database connection between tasks
- Write reusable _functions_, not operators. Write shared operators for convenience only. The main focus should be the implementation functions.
- Avoid using xcom. Use it only if it cannot be avoided.
- Write docstrings for your dag definition files (module-level) and operators
    (class-level).
- Don't use multiple tasks unless you need to.
- What to set for start_date and execute_date?

This is my opinionated view on how to use Airflow.

Airflow is a scheduler like cron, only more advanced.

## WTF is a DAG?

[Directed Acyclic Graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph)
is a fancy way of saying a tree structure. In Airflow it represents a bunch of
related tasks.

In mathematics, a graph models the relationship between objects.

A *directed graph* means the relationships have a direction. In dataflow
programming, the relationship is the *dependencies of tasks*. For example, task
might be configured to run only if and when it's upstream tasks have completed
successfully. (This is the default in Airflow). An undirected graph would have
lines connecting them with no arrow head.

And *acyclic* means there's no path leading from one node back to the same
node. So a task never runs twice in one dag run.

## Write docstrings

Write a docstring in your dag definition files and operators. For operators,
include the parameters, input files, xcom pulls and pushes.

```python
"""

"""
from airflow.models import BaseOperator

class CompleteProcessOperator(BaseOperator):
    """
    Perform a task.

    Pushes 'to xcom.
    """
```

## Don't share a database connection

Connect to the database in each task.

```python
class MyOperator(BaseOperator):

    def __init__(self, conn_id, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.conn_id = conn_id

    def execute(self, context):
        with closing(OracleHook(self.conn_id).get_conn()) as connection:
            # Use connection here

MyOperator('my_connection')
```

## Write reusable functions, not operators

If you want to share code between dags, focus on writing functions, instead of
operators, that perform the work a task will carry out.

I should be able to import your functions and use them in my own operators.

If you write an operator to reuse, keep it small and call the functions you've
written, be there for convenience.

## Avoid using Xcom.

Xcom allows you to communicate with downstream tasks, but don't overuse it. In
fact you should avoid using xcom where possible.

This is the most important part of Airflow's documentation:

> An operator describes a single task in a workflow. Operators are usually (but
> not always) atomic, meaning they can stand on their own and don’t need to share
> resources with any other operators. The DAG will make sure that operators run
> in the correct certain order; other than those dependencies, operators
> generally run independently. In fact, they may run on two completely different
> machines.

> This is a subtle but very important point: in general, if two operators need to
> share information, like a filename or small amount of data, you should consider
> combining them into a single operator. If it absolutely can’t be avoided,
> Airflow does have a feature for operator cross-communication called XCom that
> is described elsewhere in this document.

## Only pull from upstream tasks.

If you have line of concurrent tasks, and don't want to pull from another
concurrently running pipeline, specify to only pull from your upstream tasks.

```python
upstream_task_ids = [t.task_id for t in self._upstream_list]
self.xcom_pull(task_ids=task_ids, key='foo')
```
