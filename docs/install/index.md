---
layout: inner-page
title: Installation
---

Represent Boundaries is a Django app, which you can deploy on its own or integrate into an existing Django project.

## Install dependencies

Represent Boundaries requires Python 2.7, 3.3 or 3.4 and PostGIS. Follow GeoDjango's [instructions](https://docs.djangoproject.com/en/dev/ref/contrib/gis/install/), or use the quick-start guide for OS X users below.

If you have issues installing dependencies, check GeoDjango's [help section](https://docs.djangoproject.com/en/dev/ref/contrib/gis/install/#troubleshooting).

### Mac OS X

This guide assumes you are using Homebrew as your package manager. If you use MacPorts or Fink, the steps are similar.

1. [Install Xcode](https://itunes.apple.com/us/app/xcode/id497799835)
1. [Install Homebrew](brew.sh#install)
1. Ensure Homebrew is up-to-date:

        brew update

1. Ensure Homebrew is ready to go. Most warnings can be safely ignored:

        brew doctor

1. Install Python 2.7, which will install pip and setuptools:

        brew install python

1. Install GDAL and PostGIS:

        brew install gdal postgis

1. Follow the instructions to start a PostgreSQL server:

        brew info postgresql

## Install Represent Boundaries

1. Create a PostGIS database:

        createdb my_database
        psql my_database -c "CREATE EXTENSION postgis;"

1. Install Django, psycopg2 and Represent Boundaries:

        pip install Django psycopg2 represent-boundaries

1. Start a new Django project. Skip this step if you are integrating Represent Boundaries into an existing Django project.

        django-admin.py startproject my_project
        cd my_project

1. In `my_project/settings.py`, [configure the default database](https://docs.djangoproject.com/en/dev/ref/contrib/gis/tutorial/#configure-settings-py) to connect to the PostGIS database you created above.

1. In `my_project/settings.py`, add these lines to the end of the `INSTALLED_APPS` list:

        'django.contrib.gis',
        'boundaries',

1. In `my_project/urls.py`, add this line to the end of the `urlpatterns` list:

        (r'', include('boundaries.urls')),

1. From your project's directory, run:

        python manage.py syncdb --noinput

You can now run `python manage.py runserver` and navigate to [http://127.0.0.1:8000/boundary-sets/](http://127.0.0.1:8000/boundary-sets/) to see your empty API. <a href="{{ site.baseurl }}/docs/import/">Let's add some data!</a>
