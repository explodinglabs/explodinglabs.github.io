---
layout: post
category: python
date: 2017-01-16
title: "Restart Django Migrations"
permalink: /python/restart-django-migrations
redirect_from: /django/restart-migrations
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

To reset an app back to the initial "zero" migration:

```zsh
python manage.py migrate --fake myapp zero
```

Alternatively, you may want to completely start again.

Delete all migration files:

```zsh
find . -path "*migrations/*.py" -not -name __init__.py -delete
```

Now you can recreate the database and migrations:

```zsh
dropdb mydb; createdb mydb # Recreate postgres
python manage.py makemigrations
python manage.py migrate
```
