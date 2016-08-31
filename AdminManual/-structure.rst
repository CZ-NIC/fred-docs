
.. _FRED-Admin-structure:

Publication structure (Admin.Manual)
====================================

* :ref:`Installation <FRED-Admin-structure-installation>`

* Configuration
   * Overview of executables and the default config.files
      * Main and supporting programs
   * Configurable database values
     * table:enum_parameters

* Registry initialization :sup:`$READY$`
   * Setting up a zone
   * Setting up registrars
   * Setting up the invoicing subsystem
     (price list, invoice numbering, VAT tax, credit)

* Periodic tasks (CRON)
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

* Billing
   * Price list

.. Administrative tasks

* CR search (Daphne/*_admin_clients?)

* Registrar administration
   * add/delete/details/edit/block/unblock

* Domain administration (using the system registrar)
   * cancel(blacklist and delete)/block/unblock (Daphne)
   * register(create+renew)/extend(renew) (client?)
   * inclusion in a zone

* Maintenance (manual tasks)
   * Postgresql database
      * backup (regular security backup - postgresql documentation)
      * regular vacuum (check postgresql documentation)
   * Regular cleanup to keep the size of system low
      * Syslog log rotate
      * Content of /var/lib/pyfred/* (managed files)
      * Logger database content archivation (archivation of old partitions)

* Customizations
   * Localization of UIs
   * Template adaptation
   * Bank-transcript processing (custom bank)

* Extensions
   * mojeID
   * DomainBrowser
