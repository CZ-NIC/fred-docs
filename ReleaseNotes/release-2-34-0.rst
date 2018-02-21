


Version 2.34.0
==========================

.. rubric:: Enhancements

* transitioned to a newer C++ standard (C++14)
* Registrars' passwords stored as hashes
* reimplemented object deletion (object types by name, spread during time argument)
* reimplemented generation of poll messages
* documentation updates (see :doc:`record of changes </RecordOfChanges>`)

.. rubric:: Bugfixes

* hotfix in payment transcript processing (added backslash escaping of some elements)
* fixed database-level locking during some of the EPP operations
