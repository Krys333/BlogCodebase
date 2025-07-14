---
title: "Introduction to Airflow"
date: 2025-05-01
author: 
  name: "Krystian Bucko"
  image: images/author/krys.jpg
  twitter: '@KrystianBucko'
categories: ["Data Orchestration", "2025", "ETL", "highlight"]
description: "A simple introduction to Apache Airflow."
thumbnail: "images/dags_intro.png"
image: "/images/dags_intro.png"
---

## What is Apache Airflow?
Airflow is an open-source platform for programmatically scheduling and monitoring workflows. Think of it as a conductor for all your data-related tasks, making sure things happen in the right order, and at the right time.

Key features to highlight:

- Written in Python, with DAGs as workflows.
    - Workflow is made-up of individual tasks.
- Executes tasks in a defined order.
    - Supports sequential as well as parallel runs of tasks.
    - Supports retries
        - i.e. set retry count if task fails.
        - Interface for rerunning tasks at a push of a button.
    - Can handle execution order based on task outputs (i.e. skipping tasks).
- Supports logging.
- Has a concept of Pools.
    - Tasks are executed with pre-defined pools and take up pools when executing.
    - This can be used for flow control, or an intentional bottleneck.
- Integrates with cloud services.
- Has a handy visual interface.
    - Fantastic for visualising task runs.
    - Has a great interface for listing, clearing, removing and carrying out other actions on tasks with specific status.

### Example

```python
from airflow import DAG
from airflow.operators.bash import BashOperator
from datetime import datetime

with DAG(dag_id="simple_workflow",
         start_date=datetime(2023, 1, 1),
         schedule_interval="@daily",
         catchup=False) as dag:

    task1 = BashOperator(
        task_id='print_hello',
        bash_command='echo "Hello, Airflow!"'
    )

    task2 = BashOperator(
        task_id='print_date',
        bash_command='date'
    )

    task1 >> task2  # task2 runs after task1
```


### What is a Task?
A task is a single unit of work — for example, running a script, querying a database, or moving files.

Types of Tasks:

- Operators. Predefined building blocks.
    - BashOperator - can execute bash commands
    - PythonOperator - can run python scripts

- Sensors. Wait for something to happen. 
    - (e.g., a file to appear).
    - A different task to return with a specific status.


### Summary

Airflow is a great handy tool that is a game-changer in orchestration. As someone who came into Airflow from having to rely on AWS's step functions before, I cannot stress how much I like this tool. The interface, the logging, the retries. All of the features offer huge development experience improvements. I could not recommend it enough! 