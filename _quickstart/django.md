---
layout: post
title:  "Django"
description: "Hit the ground running with one of the most popular Python web frameworks."
---

[Python version: 3.7.0](https://docs.python.org/3.7/)

[Django version: 2.1.3](https://docs.djangoproject.com/en/2.1/)

Must have [Python](https://docs.python-guide.org/starting/installation/) and [Postgresql](http://postgresguide.com/setup/install.html) installed.

# Installation

```bash
python3 -m venv venv

source venv/bin/activate

pip install django
pip install ipython
pip install psycopg2

django-admin startproject SITE_NAME
python SITE_NAME/manage.py startapp APP_NAME

```

# Database set up

## Update settings.py

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'SITE_NAME',
        'USER': 'SITE_NAME',
        'PASSWORD': 'local_development_password_only',
        'HOST': 'localhost',
        'PORT': '5432'
    }
}
```

## Create the database locally

```bash
psql -c "create user SITE_NAME with password 'local_development_password_only'"
createdb -O SITE_NAME SITE_NAME;
```

## Run the Django database commands

```bash
python SITE_NAME/manage.py makemigrations
python SITE_NAME/manage.py migrate

python SITE_NAME/manage.py createsuperuser
```

# Useful commands

## Start the interactive shell

```bash
python SITE_NAME/manage.py shell
```

# Useful resources

[Django model fields](https://docs.djangoproject.com/en/2.1/ref/models/fields/)