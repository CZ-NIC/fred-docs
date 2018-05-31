
.. index:: logger, Audit

Audit log (logger)
==================

Audit log is the ability of the Registry to record user interface transactions,
who requested them, from where, and what the result was.

Among :ref:`other purposes <features-gen-auditlog>`, audit log records
are also suitable for generating Registry statistics.

.. index:: logger; disable

.. rubric:: Disabling the logger

If the Registry operator does not need audit log records, they just do not
launch the logger daemon (``fred-logd``). Most :doc:`depending components
</Architecture/TopLevelComponents/index>` will still operate without recording
the audit log data, only the *EPP Apache module* has to be re-configured
not to require it (set the option `EPPlogdMandatory` to \ `Off`).

Logged services
---------------

Logged services of user interfaces encompass (a selection of services that
are not :term:`CZ-specific` from the db table ``service``):

* EPP (infix ``epp_``)
* RDAP (infix ``rdap_``)
* Unix whois (infix ``whois_``)
* Web whois (infix ``webwhois_``)
* Public request (infix ``pubreq_``)
* Admin (infix ``admin_``)
* WebAdmin (infix ``webadmin_``)

The infixes are used to name logger database tables,
see `Database & partitioning`_.

Contents of a log record
------------------------

An audit log record is made per user request and it is composed of:

* request initiation (time_begin),
* request completion (time_end),
* service (see `Logged services`_),
* request type (further classification under the individual services),
* user name,
* source IP address,
* result (code and message),
* properties (request and reply parameters as key-value pairs).

For some activities, even the whole request and reply are logged, e.g. for EPP.

Browsing the log
----------------

The audit log records can be viewed in the web administration
(Daphne) under a user with the permission ``read.logger``.
The log records can be searched like any other records,
see :doc:`/AdminManual/AdministrativeTasks/Search`.

Database & partitioning
-----------------------

Audit log data can be stored in an independent database that can be completely
separated from the rest of FRED data, even physically, which is recommended
for better performance.

The database must be properly secured so that nobody can modify the records.

.. rubric:: Partitioning logic

The audit log data is partitioned into tables according to:

* purpose -- records are used by system admins for *monitoring*
  (infix ``mon_``) or not (empty infix),
* service (see `Logged services`_),
* date -- year as 2 digits ``YY`` and month as 2 digits ``MM``.

Which means that the db tables are named using the pattern
\ ``request_<service-infix><monitoring-infix><YY>_<MM>``
and they contain only the logs of the specified period and service.

.. rubric:: Creating partitions

New partitions can be prepared using the Python script ``create_parts``,
which is included with the package ``fred-logger-maintenance``.
If the logger needs to write into a new partition, which does not exist yet,
it will create the new partition automatically on the fly but at a cost.
Therefore, we recommend to prepare partitions in advance (e.g. for a whole year).

.. rubric:: Archiving partitions

Legislation may require to keep the records for a certain period of time
(e.g. for 2 years). Older records should be regularly removed from the database
to free system resources.

Partitions are to be archived by month using ``pg_dump`` and archived partitions
can be dropped using the Python script ``drop_parts`` afterwards. This script is
included with the package ``fred-logger-maintenance``, too.
