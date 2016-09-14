
.. _FRED-Features-General:

General features
=====================

.. only:: mode_structure

   **Sources:** WEB/Features + WIKI/Dev + WIKI/Test

   **Chapter outline:**

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
   * Technical checks
      * types :sup:`src:WIKI/Test`
   * Notifications & Reports
      * (Mailing, Messaging...)
      * Delivery channels (email, sms, letters, poll msgs)
      * types  :sup:`src:DB`
         * (group by object type? or use table?)
         * Domain Expiration Warning
         * Domain Deletion Warning
         * ...expirations, validations :sup:`ENUM`, changes, ...
         * Tech.check results (go into poll messages + contact email?)
   * IDN support (we can register domains in UTF-8 and display them, but we can't restrict the character set just to a local alphabet)
   * DNSSEC support (get keys from registrars + include them in zone file)
   * ENUM
   * Accounting (Pricing, Payments, Charging, Invoicing)

:abbr:`TBD (to be developed)`
