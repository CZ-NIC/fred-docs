


Release 2.35.0
==========================

.. rubric:: Enhancements

* changes in the database schema concerning email storage – see :doc:`./Upgrade-2-35`
   * email stored unrendered to decrease ``mail_archive`` table size
   * support for email template versioning
   * email rendered only on demand (sending, inspecting details)
   * newer minimum version of PostgreSQL required – see the :ref:`System requirements <system-reqs-aux>`
* transproc allows to restrict payment downloads with dynamic date intervals
* new fred-admin command (``--create_expired_domain`` – re-register a domain for another owner and force the domain expired)
* generation of historical record statements in Daphne

.. rubric:: Bugfixes

* fixed record statement generation for objects in ``deleteCandidate`` state
