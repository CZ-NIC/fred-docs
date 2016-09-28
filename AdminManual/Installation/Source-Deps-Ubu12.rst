
.. _Source-Deps-Ubu12:

Ubuntu 12 package list
~~~~~~~~~~~~~~~~~~~~~~
::

   apache2-threaded-dev
   autoconf-archive
   gettext
   ghostscript
   ldnsutils
   libapache2-mod-python
   libapache2-mod-wsgi
   libboost1.48-all-dev
   libcurl4-openssl-dev
   libminizip-dev
   libmpdec-dev
   libomniorb4-dev
   liborbit2-dev
   libssh-dev
   libtool
   libxml2-dev
   libxml2-utils
   libzip-dev
   make
   omniidl-python
   omniorb
   omniorb-idl
   omniorb-nameserver
   p7zip-full
   postgresql
   psmisc
   python-beaker
   python-cherrypy3
   python-clearsilver
   python-dnspython
   python-m2crypto
   python-psycopg2
   python-pygresql
   python-simplejson
   python-simpletal
   python-trml2pdf
   ssmtp
   ttf-dejavu
   ttf-freefont
   ttf-mscorefonts-installer
   whois
   xsltproc

Known issues
~~~~~~~~~~~~

.. only:: mode_structure

   .. todo:: Is this still an issue?

There may be a problem with installing :file:`libcurl4-openssl-dev`.

Following the chain of dependencies, you will find that the problematic package
is :file:`libgcrypt11-dev` (probably v. 1.5.4)—downgrade it
to the closest lower version (probably v. 1.5.0, must be >= 1.4.0), e.g.::

   $ sudo apt-get install libgcrypt-dev=1.5.0-3ubuntu0.4

Then install all the packages in the dependency chain up to *libcurl*
in this order::

   $ sudo apt-get install libgnutls-dev
   $ sudo apt-get install librtmp-dev
   $ sudo apt-get install libcurl4-openssl-dev

.. NOTE The problematic library was installed from our repositories
