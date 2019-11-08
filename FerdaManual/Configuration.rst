
Configuration
=============

Back ends required by Ferda are configured in `.conf` files.
There will be example configuration files included
(:file:`fred-registry-services.conf.example` and
:file:`fred-logger-services.conf.example`).

Ferda front end is configured as a Django project in a :file:`settings.py` file.
The following sections describe only the most critical settings.
There will be an example configuration file included
(:file:`settings.py.example`).

Connection to back end
----------------------

:samp:`FERDA_REGISTRY_NETLOC = '{host}:{port}'`
   Set up the network location of the *gRPC server* with connection
   to :program:`fred-registry-services`.

:samp:`FERDA_LOGGER_NETLOC = '{host}:{port}'`
   Set up the network location of the *gRPC server* with connection
   to :program:`fred-logger-services`.

Django apps
-----------

``INSTALLED_APPS`` must include:

- django.contrib.admin
- django.contrib.auth
- django.contrib.contenttypes
- django.contrib.sessions
- django.contrib.messages
- django.contrib.staticfiles
- django_python3_ldap (if you will use LDAP for Authentication_)
- ferda.apps.FerdaConfig

Authentication
--------------

Set an authentication back end in the ``AUTHENTICATION_BACKENDS`` variable
according to your policies or preferences.

See `User authentication in Django
<https://docs.djangoproject.com/en/2.2/topics/auth/>`_.
