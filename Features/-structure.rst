
.. _FRED-Features-structure:

Publication structure (Features)
================================

.. Note:: Features will also contain conception logic.


* General Features
   * RRR model, registrators
   * Registrations
      * Registrable objects + relationships
      * Objects states, objects life cycle
      * Object sharing
      * Object history
   * Zone generation
   * Logging
      * audit logging vs. process logging
   * Notifications & Reports (Mailing, Messaging...)
      * Delivery channels (email, sms, letters, poll msgs)
      * types (group by object type?)
         * Domain Expiration Warning
         * Domain Deletion Warning
         * ...expirations, validations :sup:`ENUM`, changes, ...
         * Tech.check results (go into poll messages)
   * Technical checks
      * types
   * Accounting (Pricing, Payments, Charging, Invoicing)
   * IDN support (we can register domains in UTF-8 and display them, but we can't restrict the character set just to a local alphabet)
   * DNSSEC support (get keys from registrars + include them in zone file)
   * ENUM

* Administration Features (~ADIF+utils)
   * System registrar (see Registrar Features)
   * Web administration :sup:`READY`
   * CLI administration (fred-admin, transproc, fred-dbmanager, genzone_client)

* Registrar Features (~RIF) – :abbr:`TBD (to be developed)`
   * EPP protocol features (standard)
      * check/create/delete... domain/contact
      * request authinfo, request tech.test (a part of std.EPP)
      * Poll messages (a part of std.EPP)
      * change registrar info? (a part of std.EPP???)
   * extended
      * check/create/delete... keyset/nsset

* Public Features (~PIF) – :abbr:`TBD (to be developed)`
   * Anonymous end-users
      * WhoisWeb, WhoisUnx, RDAP
      * restrictions (CAPTCHA)
   * Registrants (Dom.Owners), Administrative contacts (Dom.), Technical contacts (NS/Keys)
      * Notifications? (see General features)
      * Validation of contact information
      * Registry object locking (blocking transfer/all changes)
      * Authinfo provision

.. Note:: Terminology: Registrant vs. Dom.Owner vs. Dom.Holder
   
   * ICANN uses "Registrant"
   * Dom.Owner About 1,820,000 results from Google (Sept 2nd, 2016)
   * Dom.Holder About 334,000 results from Google (Sept 2nd, 2016)

.. Note:: Terminology: Accounting vs. Billing

   (from OxfordLearnersDictionaries.com)

   * accounting ... the process or work of keeping financial accounts
   * billing ... the act of preparing and sending bills to customers
   * bill is a synonym to invoice

   (from WordNet)

   * accounting ... a system that provides quantitative information about finances
   * billing ... request for payment of a debt, syn: charge

