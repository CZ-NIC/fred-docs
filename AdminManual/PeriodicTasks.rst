
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
   :backlinks: none

Zone file generation
--------------------

**Task command**::

   /usr/bin/genzone_client

**Typically launched**: every 30 minutes

**Real run time** [CZ.NIC]: ~ 5 min (.cz zone)

**Required FRED components**:

* ``pyfred``: Genzone module – zone file generation

**Other required components**: none

**Task activities**:

* generates a zone file for each configured zone


Administration of registrable objects
-------------------------------------

.. _cronjob-regular:

Regular procedure
^^^^^^^^^^^^^^^^^

.. Important:: This task is critical for Registry operation, it must be set up!

**Task command**::

   /usr/sbin/fred-admin --object_regular_procedure [--object_delete_types="contact,domain,keyset,nsset"]

**Typically launched**: at midnight (00:00) and noon (12:00)

**Real run time** [CZ.NIC]: ~ 20 min

**Required FRED components**:

* ``pyfred``: Mailer module – email generation,
  FileManager module + filemanager_client – saving expiration letters (pdf)
* ``fred-doc2pdf``: letter templates + PDF generation

**Other required components**:

* ``xsltproc``

**Task activities**:

* updates the states of the registrable objects of all types; the states
  depend on time and other states that are set manually
* notifies registrars and end users (contacts) about state changes:
   * generates poll messages to notify registrars
   * generates emails to notify contacts
   * generates letters for domain deletion warning
* generates poll messages to notify registrars about low credit
* deletes objects of selected types that have been marked for deletion
  – this activity can be disabled by omitting the ``--object_delete_types``
  argument and can be run in a separate task (see the next task)

.. _cronjob-object-deletion:

Separate object deletion
^^^^^^^^^^^^^^^^^^^^^^^^
.. Important:: This task is critical for Registry operation!

   Set this cronjob if you want to perform object deletion (or part of it)
   separately from the :ref:`cronjob-regular`.

**Task command**::

   /usr/sbin/fred-admin --object_delete_candidates <options>

**Typically launched**: at least once a day (if you delete all at once,
you can include it with the regular procedure or launch it after the regular
procedure is finished)

**Required FRED components**: none

**Other required components**: none

**Task activities**:

* deletes objects of selected types that have been marked for deletion

**Task variants**:

* deleting *all at once* (suitable for non-domains), for example:

  ::

      /usr/sbin/fred-admin --object_delete_candidates --object_delete_types="contact,keyset,nsset"

* deleting *by parts* (suitable for domains) with the ``--object_delete_parts`` option
  – this variant allows you to randomize deletion of objects by spreading it
  over several calls; this variant of the task means these activities:

   * creates a randomly-ordered list of objects (delete candidates)
   * deletes a fraction of the list, repeatedly in iterations,
     the size of the fraction is given in the  ``--object_delete_parts`` option,
     e.g. if ``--object_delete_parts=2``, a half of the list is deleted
     in a single iteration, if ``object_delete_parts=10``, a tenth of the list
     is deleted in a single iteration and so on
   * single iteration can be spread over a period of time specified in the
     ``--object_delete_spread_during_time`` argument in seconds
   * the value of ``object_delete_parts`` is calculated depending
     on CRON configuration (how often the task is run)
   * finally, deletes the rest (\ ``--object_delete_parts=1`` – this is
     the default value if the parameter is omitted)

   * *Example*: spread the deletion of domains over a whole day::

      # Iteration
      */10 1-22 * * *  /usr/sbin/fred-admin --object_delete_candidates --object_delete_types="domain" --object_delete_parts=$((((24 * 60 - (10#$(date \+"\%H") * 60 + 10#$(date \+"\%M")))/10) - 6)) --object_delete_spread_during_time=600

      # Finalization
      45 23 * * *  /usr/sbin/fred-admin --object_delete_candidates --object_delete_types="domain" --object_delete_parts=1

     **Real run time** [CZ.NIC]: ~ 5 s (one iteration)

.. _cronjob-contact-merger:

Automatic contact merger
^^^^^^^^^^^^^^^^^^^^^^^^

See also :doc:`introduction to the contact merger </Concepts/ContactMerger>`.

**Task command**::

   /usr/sbin/fred-admin --contact_merge_duplicate_auto \
      [--except_registrar <registrar-handle> ... OR --registrar <registrar-handle> ...] \
      [--selection_filter_order <filter1,filter2,filter3>] \
      [--dry_run]

**Typically launched**: once a week

.. **Real run time** [CZ.NIC]: ~ 16 minutes

**Required FRED components**:

* ``pyfred``: Mailer module
* ``fred-logd``: Logger

**Other required components**: none

**Task activities**:

* looks for duplicate contacts per registrar that can be specified as:
   * all registrars in the database except registrars given
     in ``--except_registrar`` arguments (e.g. when you don't want to merge
     contacts managed by the system registrar), or
   * only registrars given in ``--registrar`` arguments,
* :ref:`selects the best destination contact <merge-auto-criteria>`,
* :ref:`merges <merge-operation>` all *source contacts* into the *destination contact*.

Useful filters for selection of the *destination contact*:

* :abbr:`mcs_filter_max_domains_bound (contact has most domains linked as a holder or administrative contact)`
* :abbr:`mcs_filter_max_objects_bound (contact has most objects linked – domains, nssets or keysets)`
* :abbr:`mcs_filter_recently_updated (contact has been updated most recently)`
* :abbr:`mcs_filter_recently_created (contact has been created most recently)`

The procedure will apply the filters in the order specified on the command line;
if not specified, the default filters in the default order will be applied,
see the :doc:`concept </Concepts/ContactMerger>`.

The ``--dry_run`` option is available to preview what the command will do.
Also see the program ``--help`` for more options.

Automatic contact verification :sup:`CZ-specific`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _cronjob-akm:

Automatic keyset management
^^^^^^^^^^^^^^^^^^^^^^^^^^^

See also the :doc:`AKM concept </Concepts/AKM>`.

**Task command**::

   /usr/bin/fred-akm load --wipe-queue --no-secure-noauto && \
      /usr/bin/fred-akm scan && \
      /usr/bin/fred-akm notify && \
      /usr/bin/fred-akm update && \
      /usr/bin/fred-akm clean

**Typically launched**: once a day

**Real run time** [CZ.NIC]: ~ 3.5 hours

**Required FRED components**:

* ``fred-akmd``: AKM interface

**Other required components**: cdnskey-scanner

**Task activities**:

* :program:`load` – prepares a queue of domains (and corresponding name servers)
  which will be scanned for the presence of CDNSKEY records;
  Domains will be loaded either from the CORBA server (default) or an
  input file, and they can be filtered through a white list (optional).

  Domains can be selected according to their security status group:

   * insecure – domains without a keyset,
   * secure-noauto – domains secured with a manually managed keyset,
   * secure-auto – domains secured with an automatically managed keyset.

  By default, domains are selected according to all three groups but some
  of these groups can be excluded from the load with command options,
  e.g. ``--no-secure-noauto``.

  The ``--wipe-queue`` argument clears the scan queue before new tasks are enqueued.
  See also ``fred-akm load --help``.

* :program:`scan` – scans the enqueued domains by running an external tool and
  saves the scan results,
* :program:`notify` – sends notifications about initiated or broken acceptance
  period (insecure domains only),
* :program:`update` – performs requested changes on keysets and/or domains,
  notifies about key updates,
* :program:`clean` – removes scan results made obsolete by the update.

**Configuration**:

* in a configuration file

Communication
-------------
* Letters Postservis :sup:`CZ-specific`
* Letters Optys :sup:`CZ-specific`
* SMS Texts :sup:`CZ-specific`
* Registered Letters :sup:`CZ-specific`

.. _cronjob-public-requests:

Processing public requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. Note:: This procedure processes only :term:`public request`\ s for personal information.

**Task command**::

   /usr/sbin/fred-admin --process_public_requests [--types <list of public request types>]

**Typically launched**: every 5 minutes

**Required FRED components**:

* ``pyfred``: Mailer module – email generation
* ``fred-logd``: Logger interface

**Other required components**: none

**Task activities**:

* generates emails in response to :ref:`resolved <resolve-public-request>`
  public requests of types:

   * ``personalinfo_auto_pif`` – requests to send personal info to an email in the registry
     (authorized and resolved automatically),
   * ``personalinfo_email_pif`` –  requests to send personal info to another email,
     authorized with an email signed with a digital signature
     (:ref:`resolved manually <resolve-public-request>`),
   * ``personalinfo_post_pif`` – requests to send personal info to another email,
     authorized with a letter containing a notarized signature
     (:ref:`resolved manually <resolve-public-request>`).

  If the ``--types`` argument is omitted, all of the aforementioned types are processed.

Registrars
----------

Generating poll messages about request usage
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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
  of the requests over limit

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
  sends a notification with a list of registrars blocked on this day

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

.. _cronjob-contact-reminder:

Annual contact reminder
-----------------------

The goal is to remind users to review their contact details and to inform them
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
* sends them an email of the ``annual_contact_reminder`` type (see :ref:`template
  params <email-type-contact-reminder>`)

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
