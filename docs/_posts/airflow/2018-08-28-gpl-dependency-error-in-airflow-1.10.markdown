---
layout: post
title: GPL dependency error installing Airflow 1.10
category: airflow
permalink: /airflow/gpl-dependency-error-with-pip
---
When installing Airflow 1.10 with pip, I received the following error:

```
RuntimeError: By default one of Airflow's dependencies installs a GPL
dependency (unidecode). To avoid this dependency set
SLUGIFY_USES_TEXT_UNIDECODE=yes in your environment when you install or upgrade
Airflow. To force installing the GPL version set AIRFLOW_GPL_UNIDECODE
```

<div class="wide-logos" markdown="1">
![airflow](/assets/airflow.png)
</div>

As the error message explains, the solution is to **set the environment
variable** when calling pip:
```
SLUGIFY_USES_TEXT_UNIDECODE=yes pip install apache-airflow==1.10.0
```
