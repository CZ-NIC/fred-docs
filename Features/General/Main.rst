
.. _FRED-Features-General:

General features
=====================

.. only:: mode_structure

   .. struct-start

   **Sources:** WEB/Features + WIKI/Dev + WIKI/Test :ref:`??? <src>` 
   | **AoW:** 10 days

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

   .. struct-end

:abbr:`TBD (to be developed)`

The main purpose of the FRED is to provide information on domains via the DNS
(zone file) as well as in response to public queries (whois).
To accomplish this, the system allows to input the relevant information into
its database through the registration proccess and comprises the means
to administer existing data.

The relevant information obtained by the registration process is grouped
into so-called **registrable objects**.

To ensure the authenticity of the data, only authorized entities can perform
registrations and modify existing data in the Registry.

.. DNS requires an association of two or more nameservers (primary and backup)
   with a domain => nameserver set
   to enable the chain of trust in the DNS, a set of keys can be associated
   with a domain => key set
   why contacts -
   implements protocol for communication with registrars
   Thick regisrty - contains all whois information

Registry—Registrar—Registrant model
-----------------------------------

Potential domain owners (Registrants) may not be known to the Registry prior
to a registration and therefore the Registry has no means to authorize
their access to the database.

Therefore registrations and changes to existing information are mediated
by the Registrars which are organizations authorized by the Registry to request
registrations of domains and related operations over registrable objects.

Sponsoring Registrar
^^^^^^^^^^^^^^^^^^^^
Each registrable object in the Registry is managed by exactly one Registrar—the
sponsoring Registrar—and only this Registrar may modify it.

A Registrant is allowed to change the sponsoring Registrar of their registrable
object by means of a transfer process.

Registrable objects
-------------------

The registrable objects are the following:

* Domain,
* Contact (in roles of domain owners, administrative contacts or technical contacts),
* NSSet (a group of name servers), and
* KeySet (a group of DNSSEC keys).

Object relationships
^^^^^^^^^^^^^^^^^^^^

+ Object sharing

Object life cycle (states)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Object history
^^^^^^^^^^^^^^


.. Operations & Prohibitions
   -------------------------
