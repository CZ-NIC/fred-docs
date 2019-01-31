


Version 2.38.1
==========================

.. rubric:: Bugfixes

* Database:
   * fix ``mail_archive`` migration (modifies behaviour of the upgrade scripts
     ``2.32.0-2.33.0-{1,3,4}-*.sql``, see updated :doc:`./Upgrade-2-35`)
   * drop a constraint to allow multiple invoices for a single payment or
     a single invoice for multiple payments

     .. Important:: Run the upgrade script `2.35.0-2.35.1.sql
        <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.35.0-2.35.1.sql>`_,
        if you want to use :doc:`PAIN </Concepts/PAIN>` with FRED 2.38.

* Server (fred-accifd): fix search for a registrar by payment data
* Transproc: add another :term:`CZ-specific` bank connector
