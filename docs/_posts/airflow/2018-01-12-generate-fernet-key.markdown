---
layout: post
title: How to generate a Fernet key?
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

Install cryptography:
```shell
pip install cryptography
```

Generate a fernet key:
```shell
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs=
```

## Use a fernet key with Airflow

Paste the key into your `airflow.cfg`.
```
fernet_key = 81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs=
```

Alternatively, set the environment variable.
```shell
AIRFLOW__CORE__FERNET_KEY='81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs='
```

Restart Airflow's webserver.

<div class="warning" markdown="1">
For existing connections (the ones that were defined before setting the Fernet
key), you need to open each connection in the web admin, re-type the password
and save it.
</div>
