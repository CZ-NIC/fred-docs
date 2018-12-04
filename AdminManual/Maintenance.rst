
.. _FRED-Admin-Maintenance:

Maintenance
=======================

.. only:: mode_structure

   .. struct-start

   **Sources:** IVIEW + translate :ref:`??? <src>` | **AoW:** done & unplanned

   **Chapter outline:**

   * Postgresql database
      * backup (regular security backup - postgresql documentation)
      * regular vacuum (check postgresql documentation)
   * Regular cleanup to keep the size of system low
      * Syslog log rotate
      * Content of /var/lib/pyfred/* (managed files)
      * Logger database content archivation (archivation of old partitions)

   .. struct-end

This chapter should help you with the maintenance of the system,
especially the dynamic data that is generated during the system operation.

Unfortunately, specific maintenance practices depend greatly on the way
you deploy the system. However, there are some general guidelines
in this chapter that you may find useful.

.. contents:: Chapter TOC
   :local:
   :backlinks: none

Maintained dynamic data
-----------------------

There are several types of data that are generated during the operation
of the system:

* the *main* database,
* the *logger* database,
* managed files,
* syslog data.

Some of these data should be duplicated as a safety precaution or archived
if a release of system resources is required.

Most of them can be packed by a compressing archiver and moved
to a backup location (i.e. a backup server).

Databases
---------

We recommend these standard PostgreSQL's tools for database maintenance:
   * `Backup and Restore
     <https://www.postgresql.org/docs/current/static/backup.html>`_
     for database backups and
   * `Automatic Vacuuming
     <https://www.postgresql.org/docs/current/static/runtime-config-autovacuum.html>`_
     for database cleanup.

Simple backup: pg_dump
^^^^^^^^^^^^^^^^^^^^^^

Textual backup of the whole database which you may want to perform daily
using CRON. It also may come in handy in the case you need to migrate
the data to a higher version of PostgreSQL.

Recommended for both FRED databases—*main* and *logger*—as a minimum
crash-safety precaution.

See `PostgreSQL's documentation: SQL Dump
<https://www.postgresql.org/docs/current/static/backup-dump.html>`_.

Logger database content archivation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The :doc:`logger </Concepts/AuditLog>` database is divided into partitions
by months which is embedded in its schema.
This allows you to dump only the data from a specified month
(usually the previous one).

Advanced backup: continuous archiving
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Incremental binary backup that allows to recover the database to the most
recent state at a minimum cost, since it backs up at a rate of minutes
but it only records the difference from the previous backup.

Recommended for the *main* database as an advanced crash-safety precaution.

See `PostgreSQL's documentation: Continuous Archiving
<https://www.postgresql.org/docs/current/static/continuous-archiving.html>`_.



Managed files
-------------

You may archive and/or remove the older content of :file:`/var/lib/pyfred/*`
where the files managed by the FRED are located.

The system can handle missing files. When some part of the system requests
a file, that has been removed, from the file manager, it reports an exception.



Syslog data
-----------

Local syslog files can be maintained by the `logrotate` utility
which is a part of the operating system.

Syslog data on a remote log server can be maintained for example
by the `syslog-ng` application, see the `syslog-ng documentation
<https://www.balabit.com/sites/default/files/documents/syslog-ng-ose-latest-guides/en/syslog-ng-ose-guide-admin/html-single/index.html>`_
