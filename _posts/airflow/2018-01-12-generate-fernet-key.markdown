---
layout: post
date: 2018-01-12
title: Generate a Fernet key for Airflow
description:
    How to create a fernet key which is required for storing encrypted
    passwords.
category: airflow
image: /assets/airflow-wide.png
permalink: /airflow/fernet-key
---
<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

Generate a fernet key:

```shell
$ python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs=
```

Paste it into your `airflow.cfg`.

```
fernet_key = 81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs=
```
