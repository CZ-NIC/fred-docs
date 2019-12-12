


Version 2.41
==========================

See repository changelogs for larger detail.

Release 2.41.0
----------------

.. rubric:: Enhancements

* :repo:`libfred`
   - unify random numbers generator
   - lessen strictness of locking ``registrar_credit`` on initialization of
     a new record
* :repo:`rdap`
   - include standard server prohibition flags in status display
   - clean up configuration variables
* :repo:`server` -- allow invoicing registrars for the annual fee monthly
  or yearly
* :repo:`webadmin` -- allow modification of registrar handles

.. * :repo:`pyfred` -- transfer to Setuptools

.. * :repo:`utils-pyfco`, :repo:`utils-pylogger`

.. rubric:: Bugfixes

* :repo:`client` -- fix an error in the ``--version`` option
* :repo:`libfred` -- fix CMake ``libpq`` detection

..   client - fix location of certificates for development testing
