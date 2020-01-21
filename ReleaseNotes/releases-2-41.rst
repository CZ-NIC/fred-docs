


Version 2.41
==========================

See repository changelogs for larger detail.

Release 2.41.0
----------------

.. rubric:: Enhancements

* :repo:`fred-libfred`
   - unify random numbers generator
   - lessen strictness of locking ``registrar_credit`` on initialization of
     a new record
* :repo:`fred-pyfred` -- port from Distutils to Setuptools
* :repo:`fred-rdap`
   - include standard server prohibition flags in status display
   - clean up configuration variables
* :repo:`fred-server`
   - allow invoicing registrars for the annual fee monthly or yearly
   - add manpages for :program:`fred-admin`
* :file:`fred-utils-distutils` -- discontinue
* :repo:`fred-webadmin` -- allow modification of registrar handles

.. rubric:: Bugfixes

* :repo:`fred-client` -- fix an error in the ``--version`` option
* :repo:`fred-libfred` -- fix CMake ``libpq`` detection

..   client - fix location of certificates for development testing
