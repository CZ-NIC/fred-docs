
.. _FRED-Admin-PeriodicTasks:

Periodic tasks
=========================

.. only:: mode_structure

   .. struct-start

   **Sources:** WIKI/Dev + IVIEW + translate :ref:`??? <src>`
   | **AoW:** 4 days (the rest)

   **Chapter outline:**

   * *Generate zone file*
   * *Regular procedure* :sup:`CRITICAL`
      * +Delete unused objects
      * +Export notification letters (to PostServis) :sup:`CZ-specific`
      * +more (see fred-admin help)
   * *Removal of inactive records*
      * Delete expired domains :sup:`CRITICAL`
   * Perform automatic contact verifications :sup:`CZ-specific`
   * Export notification letters (to Optys) :sup:`CZ-specific`
   * Export (and send) notification SMS texts :sup:`CZ-specific`
   * Export registered letters (for manual dispatch) :sup:`CZ-specific`
   * *Generate poll messages about request usage*
   * *Block registrars over request-usage limit*
   * *Import payments and attempt pairing* :sup:`CZ-specific`
   * Invoicing :sup:`CZ-specific`
      * Generate prefixes
      * Archive (create PDF-version and assemble emails)
      * Bill registrars (charge fees and create invoice)
   * *Contact reminder* (notify for check)
   * *Generate statistics*

   .. struct-end

This chapter should help you with the setting of automated tasks in CRON.

.. contents:: Chapter TOC
   :local:

Zone file generation
--------------------

**Task command**::

   /usr/bin/genzone_client

**Typically launched**: every 30 minutes

**Real run time** [CZ.NIC]: ?

**Required FRED components**:

* ``pyfred``: Genzone module – zone file generation

**Other required components**: none

**Task activities**:

* generates a zone file for each configured zone


Administration of registrable objects
-------------------------------------

Regular procedure
^^^^^^^^^^^^^^^^^

.. Important:: This task is critical for Registry operation!

**Task command**::

   /usr/sbin/fred-admin --object_regular_procedure [--object_delete_types="1,2,3,4"]

**Typically launched**: at midnight (00:00) and noon (12:00)

**Real run time** [CZ.NIC]: ~ 20 min

**Required FRED components**:

* ``pyfred``: Mailer module – email generation,
  FileManager module + filemanager_client – saving expiration letters (pdf)
* ``fred-rifd``: EPP interface for deleting objects
* ``fred-doc2pdf``: letter templates + PDF generation

**Other required components**:

* ``xsltproc``

**Task activities**:

* updates the states of the registrable objects of all types; the states
  depend on the time and other states that are set manually
* notifies registrars and end users (contacts) about state changes:
   * generates poll messages to notify registrars
   * generates emails to notify contacts
   * generates letters for domain deletion warning
* generates poll messages to notify registrars about low credit
* deletes objects of selected types that have been marked for deletion
  – this activity can be disabled by omitting the ``--object_delete_types``
  argument and can be run in a separate task (see the next task)


Separate object deletion
^^^^^^^^^^^^^^^^^^^^^^^^
.. Important:: This procedure is critical for Registry operation!

   If the deletion of objects is not invoked within the regular procedure,
   it must be invoked separately.

**Task command**::

   /usr/sbin/fred-admin --object_delete_candidates <options>

**Typically launched**: at least once a day (if you delete all at once,
you can include it with the regular procedure or launch it after the regular
procedure is finished)

**Required FRED components**:

* ``fred-rifd``: EPP interface for deleting objects

**Other required components**: none

**Task activities**:

* deletes objects of selected types that have been marked for deletion, types:
   * 1 = contacts,
   * 2 = nssets,
   * 3 = domains,
   * 4 = keysets

**Task variants**:

* deleting *all at once*

  ::

      /usr/sbin/fred-admin --object_delete_candidates --object_delete_types="1,2,3,4"

* deleting *by parts* with the ``--object_delete_parts`` option
  – this variant allows you to randomize deletion of objects by spreading it
  over several calls; this variant of the task means these activities:

   * creates a randomly-ordered list of objects (delete candidates)
   * deletes a fraction of the list, repeatedly in iterations,
     the size of the fraction is given in the  ``--object_delete_parts`` option,
     e.g. if ``--object_delete_parts=2``, a half of the list is deleted
     in a single iteration, if ``object_delete_parts=10``, a tenth of the list
     is deleted in a single iteration and so on
   * the value of ``object_delete_parts`` is calculated depending
     on CRON configuration (how often the task is run)
   * finally deletes the rest (``--object_delete_parts=1`` – this is
     the default value if the parameter is omitted)

   * *Example*: spread the deletion of domains over a whole day::

      # Iteration
      */10 1-22 * * *  sleep $[$RANDOM\%300]
         && /usr/sbin/fred-admin --object_delete_candidates --object_delete_types="3"
         --object_delete_parts=$((((24 * 60 - (10#$(date \+"\%H") * 60 + 10#$(date \+"\%M")))/10) - 6))

      # Finalization
      45 23 * * *  /usr/sbin/fred-admin --object_delete_candidates --object_delete_types="3" --object_delete_parts=1

     **Real run time** [CZ.NIC]: ~ 5 s (one iteration)

Automatic contact verification :sup:`CZ-specific`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Communication
-------------
* Letters Postservis :sup:`CZ-specific`
* Letters Optys :sup:`CZ-specific`
* SMS Texts :sup:`CZ-specific`
* Registered Letters :sup:`CZ-specific`

Registrars
----------

Billing the fee for requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Task command**::

   /usr/sbin/fred-admin --poll_create_request_fee_messages

**Typically launched**: once a day (night time recommended, e.g. 1 AM)

**Real run time** [CZ.NIC]: ~ 10 min

**Required FRED components**:

* ``fred-logd``: Logger interface

**Other required components**: none

**Task activities**:

* generates poll messages about the usage of free EPP requests and
  if the registrar exceeded the limit, calculates the price
  for the requests over limit

**Configuration**

* in the database, table: ``request_fee_parameter``

.. _block-registrars-limit:

Blocking registrars over limit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Task command**::

   /usr/sbin/fred-admin --block_registrars_over_limit [--email support@nic.tld]

**Typically launched**: once a day

**Real run time** [CZ.NIC]: ~ 10 min

**Required FRED components**:

* ``fred-logd``: Logger interface
* ``fred-rifd``: EPP interface

**Other required components**: none

**Task activities**:

* calculates the current usage of free EPP requests and if exceeded,
  blocks the registrar's access to the Registry

   * blocks until the end of the current month
   * only if the registrar is not blocked yet and
   * only if the registrar was not unblocked in the current month yet

* disconnects all EPP sessions of the blocked registrars
* if the ``--email`` address is given and registrars were blocked,
  sends a notification with a list of registrars blocked in this batch

   .. todo:: registrars blocked in this batch or on this day???

.. Note:: In the CZ.NIC, the customer support calls the blocked registrars
   and unblocks their access on demand.

**Configuration**

* in the database, table: ``request_fee_registrar_parameter``

Import & pairing of payments
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Task command**::

   /usr/bin/transproc

**Typically launched**: depends how often you need to check for payments

**Required FRED components**:

* ``fred-admin``: the command ``--bank_import_xml`` is called
  for the import to the database

**Other required components**: none

**Task activities**:

* imports payments from all configured sources into the database
* if a payment is paired with a registrar, increases credit
  and creates an advance invoice

Invoicing
---------
* Numbering
* "Archiving" (gen. XML & PDF)
* Monthly
   * charge fee (subtract from credit)
   * bill (create invoice record)

Annual contact reminder
-----------------------

The goal is to remind users to check their contact data and to inform them
about objects linked to their contact.

**Task command**::

   /usr/sbin/fred-admin --contact_reminder [--date <date>]

The default ``<date>`` is today.
Refer to ``fred-admin --help_dates`` for acceptable date formatting.

**Typically launched**: once a day

**Real run time** [CZ.NIC]: ~ 2 min

**Required FRED components**:

* ``fred-pyfred``: Mailer interface

**Other required components**: none

**Task activities**:

* selects contacts which
   * are linked to objects,
   * were created on the day and month 300 days ago (before the specified date)
   * were not changed in the last 300 days (relatively to the specified date)
* sends them an email of the ``annual_contact_reminder`` type

Collect statistics :sup:`CZ-specific`
---------------------------------------

The statistics collector program is used in CZ.NIC to collect and export data
for the statistics server which is not a part of the FRED.

**Task command**::

   /usr/bin/collect_stats.py -s fred_daily[,mojeid_daily]

**Typically launched**: once a day (night time)

**Required FRED components**: none (database access)

**Other required components**: none

**Task activities**:

* creates CSV files that can be imported into the statistics server

.. NOTE simple_stats.py (installed from apt with fred-whois)

.. todo:: PYFRED internal periodic tasks (tech.checks, mailer) - see config
