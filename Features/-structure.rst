
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
      * Delivery channels (email, sms, letters, poll msgs, jabber, ?)
      * types (group by object type?)
         * Domain Expiration Warning
         * Domain Deletion Warning
         * ...expirations, validations :sup:`ENUM`, changes, ...
         * Tech.check results (go into poll messages)
   * Technical checks (PY)
      * types
   * (Mailing (PY))
   * (File managing (PY))
   * IDN
   * DNSSEC support (keys)
   * ENUM

* Administration Features (~ADIF+utils)
   * System registrar (see Registrar Features)
   * Web administration :sup:`READY`
   * CLI administration (fred-admin, transproc, fred-dbmanager?, other?)

* Registrar Features (~RIF)
   * EPP protocol features
      * check/create/delete... domain/contact/keyset/nsset
      * request authinfo, request tech.test (součást EPP?)
      * change registrar info? (součást EPP?)
   * Poll messages (součást EPP?)

* Public Features (~PIF)
   * Anonymous end-users
      * WhoisWeb, WhoisUnx, RDAP
      * restrictions (CAPTCHA)
   * Registrants (Dom.Owners), Administrative contacts (Dom.), Technical contacts (NS/Keys)
      * Notifications? (see General features)
      * Validation of contact information
      * Registry object locking (blocking transfer/all changes)
      * Authinfo provision
