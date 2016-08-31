
.. _FRED-Admin-structure:

Publication structure (Admin.Manual)
====================================



* System requirements ?

* :ref:`Installation <FRED-Admin-structure-installation>`

* Configuration
   * Overview of executables and the default config.files
      * Main and supporting programs
   * Configurable database values (table:enum_parameters, other?)
   * ???

* Registry initialization :sup:`$READY$`
   * Setting up a zone
   * Setting up registrars
   * Setting up the invoicing subsystem
     (price list, invoice numbering, VAT tax, credit)

* Periodic tasks (CRON) (automatic tasks)
   * Generate zone file
   * Regular procedure :sup:`$CRITICAL$`
      * +Delete unused objects
      * +Export notification letters (to PostServis) :sup:`$CZ-specific$`
   * Delete domains :sup:`$CRITICAL$`
   * Perform automatic contact verifications
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

* Accounting (Billing & Banking)
   * Price list
   * Charging fees/fines
   * Payments processing (transproc), "standard XML format?" => Dev?
   * Invoice generation :sup:`$CZ-specific$`
      * Account invoice (monthly)
      * Advance invoice (when a payment is received)
   * ???

* Notifications & Reports – anything to administer?

* Technical checks – anything to administer?

* Removal of inactive records
   * Expired domains
   * Unused contacts
   * Unused NS sets
   * Unused key sets

* CR search (Daphne/*_admin_clients?)

* Registrar administration
   * add/delete/details/edit/block/unblock

* Domain administration (using the system registrar)
   * cancel(blacklist and delete)/block/unblock (Daphne)
   * register(create+renew)/extend(renew) (client?)
   * inclusion in a zone

* Zone generation (manual)
* Technical checks execution (manual)
* Contact verification (manual)

* Maintenance (manual tasks)
   * Syslog log rotate
   * Logger database backups
   * ???

* Customizations
   * Localization of UIs
   * Template adaptation
   * Bank transcript processing (custom bank)

* Extensions
   * mojeID
   * DomainBrowser
