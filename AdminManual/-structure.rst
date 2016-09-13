
.. _FRED-Admin-structure:

Publication structure (Admin.Manual)
====================================

* **Prerequisities** (to understand this manual) :sup:`src:SELF`

* :ref:`Installation <FRED-Admin-structure-installation>` :sup:`src:WEB/Install+NOTES`

* **Configuration** :sup:`src:NOTES+IVIEW`
   * Overview of executables and the default config.files
      * Main and supporting programs with short descriptions
      * List of config.files with default locations
   * Configurable database values
      * table:enum_parameters
      * example of SQL query to change a value

* **Registry initialization** :sup:`READY, may need a revision`
   * Setting up a zone
   * Setting up registrars
   * Setting up the invoicing subsystem
     (price list, invoice numbering, VAT tax, credit)

* **Periodic tasks (CRON)** :sup:`src:WIKI/Dev+IVIEW+translate`
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

* **Administrative tasks** :sup:`src:HELP+SELF`

   * Registrar administration
      * add/delete/details/edit/block/unblock
         * access to a zone
         * authentication data
      * assign a payment

   * Objects administration
      * cancel(blacklist and delete)/block/unblock (Daphne)
      * register(create+renew)/extend(renew) (client)
      * inclusion in a zone/exclusion from a zone

      * Contact administration :sup:`$CZ-specific$`
         * View automatic verification results
         * Resolve manual verification

      * Resolving public requests

   * Object search (Daphne)

* **Accounting tasks** :sup:`src:NOTES`
   * Changing prices
   * Adding credit
   * Invoice numbering

* **Maintenance** :sup:`src:IVIEW`
   * (depends on deployment?)
   * Postgresql database
      * backup (regular security backup - postgresql documentation)
      * regular vacuum (check postgresql documentation)
   * Regular cleanup to keep the size of system low
      * Syslog log rotate
      * Content of /var/lib/pyfred/* (managed files)
      * Logger database content archivation (archivation of old partitions)

* **Customization** :sup:`src:WEB/Docs+IVIEW`
   * Localization of UIs
   * Template adaptation
   * Bank-transcript processing (custom bank)

* **Extensions** :sup:`src:WEBS+WIKI/Test`
   * mojeID
   * DomainBrowser
