:orphan:


How to migrate email data to FRED 2.35
======================================

This article describes migration of email data to the newer version
because it requires special treatment in comparison to usual upgrades.

.. Important:: We highly recommend to try out the migration in a testing environment first!

Database upgrade in this version is done in four steps to which four separate upgrade scripts correspond
and they are to be run in the order as they are numbered.
The first (`1 <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.32.0-2.33.0-1-schema-reworked.sql>`_)
and the last (`4 <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.32.0-2.33.0-4-final-drops.sql>`_)
can be run safely as they are, but the middle two scripts concerning migration
(`2 <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.32.0-2.33.0-2-migrate-without-mail-archive.sql>`_,
`3 <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.32.0-2.33.0-3-migrate-mail-archive.sql>`_)
require more attention.

.. Caution:: The last script (4) is destructive! Besides adding some new constraints,
   it deletes columns and tables that are no longer needed. Before running it,
   double-check that you have migrated all necessary data!

Email templates migration (2)
-----------------------------

To simplify template versioning, the possibility of several templates per email type
(the mapping ``mail_type_template_map``) is **discontinued**.

Before you proceed with migration, find out the cardinality of the relationship
between the *email type* (\ ``mail_type``) and the *email template* (\ ``mail_templates``),
e.g. with this query which will tell whether there is more than one template for any email type:

.. code-block:: sql

   SELECT count(*)
     FROM mail_type_template_map
     GROUP BY typeid
     HAVING count(*) > 1;

If the cardinality is 1:1 (the query returned nothing), you may just run the
script ``2.32.0-2.33.0-2-migrate-without-mail-archive.sql``.

Otherwise, the migration to the new ``mail_template`` table must be done in a way
that each email type has just one template.

Email archive migration (3)
---------------------------

The ``mail_archive`` table no longer contains complete emails but only headers
and body parameters passed in the JSON format from ``pyfred-mailer``.

.. rubric:: Full migration

.. versionchanged:: 2.38.1

   Full-migration functions, which were designed for the :term:`CZ-specific` migration
   (based on default email templates), were **discontinued**.
   If you want to migrate body parameter values together with headers,
   you must write your own function(s) first.

.. rubric:: Headers-only migration (default)

This option is handy if you want to keep just the information to whom the email has been sent.
The following function from the script ``2.32.0-2.33.0-3-migrate-mail-archive.sql``
can be used (after adaptation if necessary):

.. code-block:: sql

   migrate_mail_header(message TEXT) RETURNS JSONB

Migrated headers of sent emails by default: ``To``, ``Cc``, ``Bcc``, ``Message-ID``

Migrated headers of non-delivery reports by default
(function *migrate_mail_archive_response_to_json_impl*):
``To``, ``Data``, ``Action``,
``Status``, ``Subject``, ``Remote-MTA``, ``Reporting-MTA``, ``Diagnostic-Code``,
``Final-Recipient``

.. versionchanged:: 2.38.1

   The migration is executed within the script.

.. rubric:: No migration

If you don't want to migrate archived messages, you may back-up (if necessary)
and then remove the ``mail_archive.message`` column, but you must also set records
in the ``mail_archive.message_params`` column to the empty JSON object ``{}``
for those emails due to the ``NOT NULL`` constraint.
