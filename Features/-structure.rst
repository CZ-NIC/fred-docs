
.. _FRED-Features-structure:

Publication structure (Features)
================================

.. Note:: Features will also contain conception logic.


* **General Features** :sup:`src:WEB/Features + WIKI/Dev + WIKI/Test`
   * RRR model, registrars
   * Registrations
      * Registrable objects + relationships
      * Objects states, objects life cycle
      * Object sharing
      * Object history
   * Zones
      * generation
   * Logging :sup:`src:NOTES`
      * audit logging vs. process logging
         * explain difference, link to Admin/Config
   * Notifications & Reports
      * (Mailing, Messaging...)
      * Delivery channels (email, sms, letters, poll msgs)
      * types  :sup:`src:DB`
         * (group by object type? or use table?)
         * Domain Expiration Warning
         * Domain Deletion Warning
         * ...expirations, validations :sup:`ENUM`, changes, ...
         * Tech.check results (go into poll messages + contact email?)
   * Technical checks
      * types :sup:`src:WIKI/Test`
   * IDN support (we can register domains in UTF-8 and display them, but we can't restrict the character set just to a local alphabet)
   * DNSSEC support (get keys from registrars + include them in zone file)
   * ENUM
   * Accounting (Pricing, Payments, Charging, Invoicing)

* **Administration Features** (~ADIF+utils)
   * System registrar :sup:`src:NOTES`
      * explain concept
      * (link to Registrar Features)
   * Web administration :sup:`READY, may need a revision`
   * CLI administration (fred-admin, transproc, fred-dbmanager, genzone_client, other?) :sup:`src:HELP`

* **Registrar Features** (~RIF) – :abbr:`TBD (to be developed)`
   * EPP protocol features (standard)
      * check/create/delete... domain/contact
      * request authinfo, request tech.test (a part of std.EPP)
      * Poll messages (a part of std.EPP)
      * change registrar info? (a part of std.EPP???)
   * extended
      * check/create/delete... keyset/nsset

* **Public Features** (~PIF) – :abbr:`TBD (to be developed)`
   * Anonymous end-users
      * WhoisWeb, WhoisUnx, RDAP
      * restrictions (CAPTCHA)
   * Registrants (Dom.Owners), Administrative contacts (Dom.), Technical contacts (NS/Keys)
      * Notifications? (see General features)
      * Validation of contact information
      * Registry object locking (blocking transfer/all changes)
      * Authinfo provision

.. Note:: **Terminology: Registrant vs. Dom.Owner vs. Dom.Holder**

   * ICANN uses "Registrant"
   * "Domain Owner" About 1,820,000 results from Google (Sept 2nd, 2016)
   * "Domain Holder" About 334,000 results from Google (Sept 2nd, 2016)

.. Note:: **Terminology: Accounting vs. Billing**

   (from OxfordLearnersDictionaries.com)

   * accounting ... the process or work of keeping financial accounts
   * billing ... the act of preparing and sending bills to customers
   * bill is a synonym to invoice

   (from WordNet)

   * accounting ... a system that provides quantitative information about finances
   * billing ... request for payment of a debt, synonym: charge
