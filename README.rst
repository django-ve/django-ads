Django Ads Management System
============================

.. start-badges

.. list-table::
    :stub-columns: 1

    * - docs
      - |django30x-docs| |help|
    * - tests
      - | |python37| |django30x| |travis| |coverall|
    * - license
      - |github-license|
    * - release
      - |release-pypi|
    * - contribute
      - |github-issues| |github-forks| |github-contributors|
    * - share
      - |share-twitter| |github-stars|

.. |django30x-docs| image:: http://img.shields.io/badge/3.0-docs-0c4b33.svg?style=flat&colorA=8F8F8F
    :target: https://docs.djangoproject.com/en/3.0/
    :alt: Django 3.0 Documentation

.. |help| image:: http://img.shields.io/badge/master-forum-0c4b33.svg?style=flat&colorA=8F8F8F
    :target: https://forum.djangoproject.com/
    :alt: Django Forum

.. |share-twitter| image:: https://img.shields.io/twitter/url?url=https%3A%2F%2Fgithub.com%2Frazisayyed%2Fdjango-ads
    :target: https://twitter.com/intent/tweet?text=Download%20and%20use%20%27django-ads%27%20package%20for%20ads%20management%20with%20Python%20via%20Web%20https://github.com/razisayyed/django-ads
    :alt: Share at Twitter

.. |github-contributors| image:: https://img.shields.io/github/contributors/razisayyed/django-ads.svg
    :target: https://github.com/razisayyed/django-ads/graphs/contributors
    :alt: Github Contributors

.. |github-license| image:: https://img.shields.io/github/license/razisayyed/django-ads.svg
    :target: https://github.com/razisayyed/django-ads/blob/master/LICENSE
    :alt: Github License

.. |release-pypi| image:: http://img.shields.io/badge/Release-PyPi-0c4b33.svg?style=flat&colorA=8F8F8F
    :target: https://pypi.org/project/django-ads/
    :alt: django-ads Release on PyPi

.. |github-issues| image:: https://img.shields.io/github/issues/razisayyed/django-ads
    :target: https://github.com/razisayyed/django-ads/issues
    :alt: Github Issues

.. |github-forks| image:: https://img.shields.io/github/forks/razisayyed/django-ads
    :target: https://github.com/razisayyed/django-ads/network/members
    :alt: Github Forks

.. |github-stars| image:: https://img.shields.io/github/stars/razisayyed/django-ads
    :target: https://github.com/razisayyed/django-ads/stargazers
    :alt: Github Favorites

.. |python37| image:: https://img.shields.io/badge/Python-3.7-blue
    :target: https://www.python.org/downloads/release/python-375/
    :alt: Python 3.7.5 version

.. |django30x| image:: https://img.shields.io/badge/Django-3.0-blue
    :target: https://github.com/django/django/tree/stable/3.0.x
    :alt: Odoo 13 version

.. |travis| image:: https://travis-ci.org/razisayyed/django-ads.svg?branch=master
    :target: https://travis-ci.org/razisayyed/django-ads
    :alt: Travis-CI Build Status

.. |coverall| image:: https://coveralls.io/repos/github/razisayyed/django-ads/badge.svg?branch=master
    :target: https://coveralls.io/github/razisayyed/django-ads?branch=master
    :alt: Coveralls Checkout Status

.. end-badges


a Django Application to make it easy to add Simple (Image) Advertisements to your project.

Each Ad has a **title**, a **URL** to redirect to, an **image** to be displayed in the template as a link, a **start & end dates**, and a **weight** relative to other Ads in the same zone. The higher the weight, the more frequently the Ad will be displayed.

Each time an Ad is displayed an **Impression** will be saved to the database about it with session id and source ip address, and each time it will be clicked a **click** will be saved in the database about it with the same info.


Requirements:
-------------

- Python 3.7 or higher.

- Django 3.0.8 or higher.


Installation:
-------------

Install the package using pip:

.. code-block:: console

  pip install django-ads


Configuration:
--------------

Add ``'ads.apps.AdsConfig',`` to your ``INSTALLED_APPS``

.. code-block:: python

  INSTALLED_APPS = (
      ...
      'ads.apps.AdsConfig',
  )

Make sure ``django.template.context_processors.request`` is included in ``context_processors``

.. code-block:: python

  TEMPLATES = [
      {
          'BACKEND': 'django.template.backends.django.DjangoTemplates',
          'DIRS': [],
          'APP_DIRS': True,
          'OPTIONS': {
              'context_processors': [
                  ...
                  'django.template.context_processors.request',
                  ...
              ],
          },
      },
  ]


Make sure ``django.contrib.sessions.middleware.SessionMiddleware`` is included to ``MIDDLEWARE`` in
Django 1.10 (new style)

.. code-block:: python

  MIDDLEWARE = [
      ...
      'django.contrib.sessions.middleware.SessionMiddleware',
      ...
  ]

Make sure ``django.contrib.sessions.middleware.SessionMiddleware`` is included to ``MIDDLEWARE_CLASSES``
prior to Django 1.10

.. code-block:: python

  MIDDLEWARE_CLASSES = [
      ...
      'django.contrib.sessions.middleware.SessionMiddleware',
      ...
  ]

Add the following to your settings file:

.. code-block:: python

    gettext = lambda s: s

    ADS_GOOGLE_ADSENSE_CLIENT = None  # 'ca-pub-xxxxxxxxxxxxxxxx'

    ADS_ZONES = {
        'header': {
            'name': gettext('Header'),
            'ad_size': {
                'xs': '720x150',
                'sm': '800x90',
                'md': '800x90',
                'lg': '800x90',
                'xl': '800x90'
            },
            'google_adsense_slot': None,  # 'xxxxxxxxx',
            'google_adsense_format': None,  # 'auto'
        },
        'content': {
            'name': gettext('Content'),
            'ad_size': {
                'xs': '720x150',
                'sm': '800x90',
                'md': '800x90',
                'lg': '800x90',
                'xl': '800x90'
            },
            'google_adsense_slot': None,  # 'xxxxxxxxx',
            'google_adsense_format': None,  # 'auto'
        },
        'sidebar': {
            'name': gettext('Sidebar'),
            'ad_size': {
                'xs': '720x150',
                'sm': '800x90',
                'md': '800x90',
                'lg': '800x90',
                'xl': '800x90'
            }
        }
    }

    ADS_DEFAULT_AD_SIZE = '720x150'

    ADS_DEVICES = (
        ('xs', _('Extra small devices')),
        ('sm', _('Small devices')),
        ('md', _('Medium devices (Tablets)')),
        ('lg', _('Large devices (Desktops)')),
        ('xl', _('Extra large devices (Large Desktops)')),
    )
    
    ADS_VIEWPORTS = {
        'xs': 'd-block img-fluid d-sm-none',
        'sm': 'd-none img-fluid d-sm-block d-md-none',
        'md': 'd-none img-fluid d-md-block d-lg-none',
        'lg': 'd-none img-fluid d-lg-block d-xl-none',
        'xl': 'd-none img-fluid d-xl-block',
    }


Where each element in ``ADS_ZONES`` defines a ``zone`` that can be used in your templates to display ads. Each zone must have a name to be used in the admin interface when adding ads, and sizes to be used to display the ad images in templates.

This app has one template: ``ads/tags/render_ads_zone.html``. It makes some assumptions:

#. Your project uses Bootstrap (the ``visible-*`` and ``img-responsive`` CSS classes are used).

#. If you are using Google AdSense‎, it is assumed that you have ``'sekizai'`` in your ``INSTALLED_APPS`` and that your base template contains ``{% render_block "js" %}``.

If either of the above assumptions will cause a problem in your project, feel free to override the template.

Create a URL pattern in your ``urls.py``:

.. code-block:: python

  from django.conf.urls import include, url

  urlpatterns = [
      ...
      url(r'^ads/', include('ads.urls')),
      ...
  ]


Run Migration:
--------------

Run django Migration to add tables to your database:

.. code-block:: python

  python manage.py migrate ads


Usage:
------

Add Advertisers, Categories, and Ads using Django admin interface.

load ``ads_tags`` in your template:

.. code-block:: python

  {% load ads_tags %}

use ``render_ads_zone`` in your template where you want your ads to appear:

.. code-block:: python

  {% render_ads_zone 'zone_name' %}

use ``get_ads_count`` in your template to check if any zone has active ads.

.. code-block:: python

  {% get_ads_count 'zone1' as ads_count %}
  {{ get_ads_count 'zone1,zone2,zone3' as ads_count %}


Changelog:
----------

1.1.2 (unreleased): (Special Thanks to `@macagua <https://github.com/macagua>`_).

- add spanish translation
- add more improvements about i18n
- add Django 3.0 support
- update README file


1.1.1 (2020-03-20):

- remove @python_2_unicode_compatible (removed in Django 3.0)

1.1.0 (2019-07-28):

- get_ads_count template tag added.
- fixed setup dependency (django-js-reverse has been added).

1.0.0 (2019-03-26):

- major change in functionality (switch to JS approach in rendering templates). You need jquery to be installed in frontend to use django-ads.
- Note: templates/ads/tags/render_ads_zone.html has been changed. If you use a custom template, then please take a look at the new version.

0.2.1 (2018-07-26): (Special Thanks to `@GabrielDumbrava <https://github.com/GabrielDumbrava>`_
)

- get_zones_choices now return choices sorted based on key
- Ad, Category, and Advertizer now stay on DB after deleting `created_by` user.
- fix get_absolute_url in Ad model.
- Add `ad` and `ad__zone` filters to impressions and clicks admin pages.
- Fix clicks and impressions admin search.

0.2.1 (2018-02-05):

- add long_description to setup.py

0.2.0 (2018-02-05): (Special Thanks to `@ataylor32 <https://github.com/ataylor32>`_
)

- add Django 2.0 support
- add missing dependency (Pillow)
- update README

0.1.8 (2017-06-24):

- fix googleads script tags to load multiple ad units in the same page

0.1.7 (2017-06-24):

- Please do not use this version

0.1.6 (2017-06-24):

- fix django-sekizai dependency version

0.1.5 (2017-06-24):

- add google adsense fallback

0.1.4 (2017-03-01):

- get client ip address from HTTP_X_FORWARDED_FOR if it exists.

0.1.3 (2017-02-08):

- remove dependency on easy-thumbnails.
- add Image validation to validate image size on upload using Admin interface.

0.1.2 (2017-02-08):

- add AdImage model to allow responsive ads.

0.1.1 (2016-12-20):

- add missing templates directory.


Contribute
==========

- Issue Tracker: https://github.com/razisayyed/django-ads/issues
- Source Code: https://github.com/razisayyed/django-ads


License
=======

- The project is licensed under the Apache Software License Version 2.0.
