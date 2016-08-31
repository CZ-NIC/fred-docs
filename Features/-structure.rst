
.. _FRED-Features-structure:

Publication structure (Features)
================================

.. Note:: Features will also contain concepts of operations.


* General Features/CR Features
   * Registrations
      * Registrable objects + relationships
      * Objects states, objects life cycle
      * Object sharing
      * Object history
   * Zone generation (PY)
   * Logging
      * "audit" logging vs. process logging
   * Accounting (Pricing, Payments, Charging, Invoicing)
   * Notifications & Reports (Mailing, Messaging...)
      * Delivery channels (email, sms, letters, poll msgs)
      * types (group by object type?)
         * Domain Expiration Warning
         * Domain Deletion Warning
         * ...expirations, validations :sup:`ENUM`, changes, ...
         * Tech.check results (go into poll messages)
   * Technical checks (PY)
      * types
   * IDN
   * DNSSEC support (get keys from registrars + include them in zone file)
   * ENUM

* Administration Features (~ADIF+utils)
   * System registrar (see Registrar Features)
   * Web administration :sup:`READY`
   * CLI administration (fred-admin, transproc, fred-dbmanager?, other?)

* Registrar Features (~RIF) - :abbr:`TBD (to be developed)`
   * EPP protocol features
      * check/create/delete... domain/contact/keyset/nsset
      * request authinfo, request tech.test (a part of std.EPP)
      * change registrar info? (a part of std.EPP???)
   * Poll messages (a part of std.EPP)

* Public Features (~PIF) - :abbr:`TBD (to be developed)`
   * Anonymous end-users
      * WhoisWeb, WhoisUnx, RDAP
      * restrictions (CAPTCHA)
   * Registrants (Dom.Owners), Administrative contacts (Dom.), Technical contacts (NS/Keys)
      * Notifications? (see General features)
      * Validation of contact information
      * Registry object locking (blocking transfer/all changes)
      * Authinfo provision
