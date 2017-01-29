For a year I've tried to work with the maintainer of this program. It has/had numerous thread saftey issues. If you put the version from pip in production with users on multiple threads, variables in django-sitetree would leak between requests. The maintaner did fix some of the issues I brought up but he made others worse. In the current master branch, modifications only take place in one thread, leaving the other threads with stale sitetrees. I don't know if hes tested it in production. The only place that would work is runserver. It may be that the developer does not have an actual web server to test his builds on. He was not interested in hearing these issues and disregarded them. You can see where I finally got fed up with trying to reason this developer here: https://github.com/idlesign/django-sitetree/issues/182

This code fixes all the thread saftey issues. I use it daily in production without issue. It preserves the in memory caching by keeping a cache in each thread without leaking it between requests.

These issues may be resolved in the main branch by the time you read this.

The official readme is below.

django-sitetree
===============
http://github.com/idlesign/django-sitetree

.. image:: https://img.shields.io/pypi/v/django-sitetree.svg
    :target: https://pypi.python.org/pypi/django-sitetree

.. image:: https://img.shields.io/pypi/dm/django-sitetree.svg
    :target: https://pypi.python.org/pypi/django-sitetree

.. image:: https://img.shields.io/pypi/l/django-sitetree.svg
    :target: https://pypi.python.org/pypi/django-sitetree

.. image:: https://img.shields.io/coveralls/idlesign/django-sitetree/master.svg
    :target: https://coveralls.io/r/idlesign/django-sitetree

.. image:: https://img.shields.io/travis/idlesign/django-sitetree/master.svg
    :target: https://travis-ci.org/idlesign/django-sitetree

.. image:: https://landscape.io/github/idlesign/django-sitetree/master/landscape.svg?style=flat
   :target: https://landscape.io/github/idlesign/django-sitetree/master


What's that
-----------

*django-sitetree is a reusable application for Django, introducing site tree, menu and breadcrumbs navigation elements.*

Site structure in django-sitetree is described through Django admin interface in a so called site trees.
Every item of such a tree describes a page or a set of pages through the relation of URI or URL to human-friendly title. Eg. using site tree editor in Django admin::

  URI             Title
    /             - Site Root
    |_users/      - Site Users
      |_users/13/ - Definite User


Alas the example above makes a little sense if you have more than just a few users, that's why django-sitetree supports Django template tags in item titles and Django named URLs in item URIs.
If we define a named URL for user personal page in urls.py, for example, 'users-personal', we could change a scheme in the following way::

  URI                           Title
    /                           - Site Root
    |_users/                    - Site Users
      |_users-personal user.id  - User Called {{ user.first_name }}

After setting up site structure as a sitetree you should be able to use convenient and highly customizable site navigation means (menus, breadcrumbs and full site trees).
User access to certain sitetree items can be restricted to authenticated users or more accurately with the help of Django permissions system (Auth contrib package).


Documentation
-------------

http://django-sitetree.readthedocs.org/
