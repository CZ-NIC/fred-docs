
.. _FRED-Admin-PeriodicTasks:

Periodic tasks
=========================

.. only:: mode_structure

   .. struct-start

   **Sources:** WIKI/Dev + IVIEW + translate :ref:`??? <src>` 
   | **AoW:** 7 days (translation)

   **Chapter outline:**

   * Generate zone file
   * Regular procedure :sup:`$CRITICAL$`
      * +Delete unused objects
      * +Export notification letters (to PostServis) :sup:`$CZ-specific$`
      * +more (see fred-admin help)
   * Removal of inactive records
      * Delete expired domains :sup:`$CRITICAL$`
   * Perform automatic contact verifications :sup:`$CZ-specific$`
   * Export notification letters (to Optys) :sup:`$CZ-specific$`
   * Export (and send) notification SMS texts :sup:`$CZ-specific$`
   * Export registered letters (for manual dispatch) :sup:`$CZ-specific$`
   * Generate poll messages about request usage
   * Block registrars over request-usage limit
   * Import payments and attempt pairing :sup:`$CZ-specific$`
   * Invoicing :sup:`$CZ-specific$`
      * Generate prefixes
      * Archive (create PDF-version and assemble emails)
      * Bill registrars (charge fees and create invoice)
   * Generate statistics

   .. struct-end

:abbr:`TBD (to be developed)`

This chapter should help you with the setting of automated tasks in CRON.

.. TODO translate https://admin.nic.cz/wiki/developers/fred/cron_jobs
.. NOTE Jirka slibil doplnit

.. NOTE výpis z produkce:
   /home/lenny/Documents/Documenting/FRED/admin/cron jobs/


Zone file generation
--------------------




Administration of registry objects
----------------------------------

Regular procedure
^^^^^^^^^^^^^^^^^
(with/out object removal)

Inactive record removal
^^^^^^^^^^^^^^^^^^^^^^^

Automatic contact verification :sup:`$CZ-specific$`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Communication
-------------
* Letters Postservis :sup:`$CZ-specific$`
* Letters Optys :sup:`$CZ-specific$`
* SMS Texts :sup:`$CZ-specific$`
* Registered Letters :sup:`$CZ-specific$`
* Email assembly ?

Registrars
----------

* Bill fee (poll msgs)
* Block over (request-usage) limit
   + Send list of blocked to an (customer support) email
* Process bank transcripts

Invoicing
---------
* Numbering
* "Archiving" (gen. XML & PDF)
* Monthly
   * charge fee (subtract from credit)
   * bill (create invoice record)

Statistics
----------
