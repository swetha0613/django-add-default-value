Django Add Default Value
========================

Django Migration Operation that can be used to transfer a field's default value
to the database scheme.

[![PyPi](https://img.shields.io/pypi/v/django-add-default-value.svg?branch=master)](https://pypi.python.org/pypi/django-add-default-value/)
[![License](https://img.shields.io/github/license/3yourmind/django-add-default-value.svg)](./LICENSE)
[![Contributing](https://img.shields.io/badge/PR-welcome-green.svg)](https://github.com/3YOURMIND/django-add-default-value/pulls)
[![3yourminD-Careers](https://img.shields.io/badge/3YOURMIND-Hiring-brightgreen.svg)](https://www.3yourmind.com/career)
[![Stars](https://img.shields.io/github/stars/3YOURMIND/django-add-default-value.svg?style=social&label=Stars)](https://github.com/3YOURMIND/django-add-default-value/stargazers)


Dependencies
------------

* MySQL (or compatible)
* PostgreSQL
* Microsoft SQL Server

Installation
------------
``pip install django-add-default-value``

You can then use ``AddDefaultValue`` in your migration file to transfer the default
values to your database. Afterwards, it's just the usual ``./manage.py migrate``.

Usage
-----

Add this manually to a autogenerated Migration, that adds a new fiels::

    AddDefaultValue(
        model_name='my_model',
        name='my_field',
        value='my_default'
    )


Example
-------

Given the following migration::

    operations = [
        migrations.AddField(
            field=models.CharField(default='my_default', max_length=255),
            model_name='my_model',
            name='my_field',
        ),
    ]

Modify the migration to add a default value::


    +from django_add_default_value import AddDefaultValue
    +
     operations = [
         migrations.AddField(
             field=models.CharField(default='my_default', max_length=255),
             model_name='my_model',
             name='my_field',
         ),
    +    AddDefaultValue(
    +        model_name='my_model',
    +        name='my_field',
    +        value='my_default'
    +    )
     ]

If you check ``python manage.py sqlmigrate [app name] [migration]``,
you will see that the default value now gets set.

Contributing
------------

First of all, thank you very much for contributing to this project. Please base
your work on the ``master`` branch and target ``master`` in your pull request.

There are a few packages needed on the host system. For ubuntu the following
commands will install these

```text
apt-get install freetds-dev unixodbc-dev tdsodbc
```
Then add the following text to `/etc/odbcinst.ini`:
```ini
[FreeTDS]
Description=FreeTDS unixODBC Driver
Driver=/usr/lib/x86_64-linux-gnu/odbc/libtdsodbc.so
Setup=/usr/lib/x86_64-linux-gnu/odbc/libtdsS.so
```

Roadmap
-------
0.1: Better and maintainable packaging
0.3: Tests work with tox. Supported platforms / versions frozen
0.5: Solid tests integrated with Travis or similar CI pipeline
0.9: Final API changes preparing for 1.0
1.0: API freeze

License
-------

``django-add-default-value`` is released under the Apache 2.0 License.


