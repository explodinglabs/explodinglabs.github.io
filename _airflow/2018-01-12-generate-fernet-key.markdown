---
layout: post
title: "Generate a Fernet key for Airflow"
date: 2018-01-12
permalink: /airflow/fernet-key
---

Generate a fernet key:
```python
python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"
81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs=
```

Put it into your airflow.cfg.
```
fernet_key = 81HqDtbqAywKSOumSha3BhWNOdQ26slT6K0YaZeZyPs=
```
