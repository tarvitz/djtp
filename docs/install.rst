Installation
============

.. contents::
  :local:
  :depth: 2

Dependecies
-----------
List of whole dependencies split into backend and frontend ones.
But before start you should install of check your list for this software:

*requirements list*

1. python 2.7, 3.3, 3.4
2. nodejs-0.10.x with npm (bower for js/css deps)
3. psycopg2 for PostgreSQL databases connection
4. python-mysql for MySQL/MariaDB

*optional*

3. python-virtualenv or pip

Backend dependencies
~~~~~~~~~~~~~~~~~~~~
Backend store as pip requirement file, placed in ``requirements/base.txt`` folder.
You can install using:

.. code-block:: bash

    user@localhost template$ pip install -r requirements/base.txt

for automatic installation or install listed packages by yourself.

``requirements/docs.txt`` contains dependence list for building documents for this project.
It's not required for the proper run or work, so it could be treat as additional package deps.

Frontend dependencies
~~~~~~~~~~~~~~~~~~~~~
Nodejs ``bower`` had been chosen as frontend dependecies package manager. So you can install it
via ``npm install -g bower`` and install frontend dep list:

.. code-block:: bash

    user@localhost template$ bower install

Configuration and first run
---------------------------
**Step 1**

Tune/set up you database connection, store you settings into the
``settings/local.py`` file, for example::

    DATABASES = {
        'default': {
            # Add 'postgresql_psycopg2', 'mysql', 'sqlite3' or 'oracle'.
            'ENGINE': 'django.db.backends.postgresql_psycopg2', # Add 'postgresql_psycopg2', 'postgresql', 'mysql', 'sqlite3' or 'oracle'.
            'NAME': 'template',                      # Or path to database file if using sqlite3.
            'USER': 'user',                      # Not used with sqlite3.
            'PASSWORD': 'password',                  # Not used with sqlite3.
            'HOST': 'localhost',                      # Set to empty string for localhost. Not used with sqlite3.
            'PORT': '5432',                      # Set to empty string for default. Not used with sqlite3.
        }
    }

or leave default settings which use sqlite engine.

**Step 2**

run ``./manage.py syncdb --migrate`` script from the top level of your project:

.. code-block:: bash

    root@localhost template# npm install -g bower
    user@localhost template$ python ./manage.py syncdb --migrate

**Step 3**

run submodules initialization and update them

.. code-block:: bash

    user@localhost template$ git submodule init media/less/select2-bootstrap-css
    user@localhost template$ git submodule update media/less/select2-bootstrap-css
    ...

**Step 4**

compile bootstrap css file from less scheme one

.. code-block:: bash

    user@localhost template$ lessc --yui-compress --no-color media/less/bootstrap.less > media/css/bootstrap.css

**Step 5**

run dev server then open `url <localhost:8000>`_ in your browser

.. code-block:: bash

    (venv) user@localhost template$ python ./manage.py runserver 0.0.0.0:8000
