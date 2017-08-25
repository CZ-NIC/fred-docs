
.. _FRED-Features-General:

General features
=====================

.. only:: mode_structure

   .. struct-start

   **Sources:** WEB/Features + WIKI/Dev + WIKI/Test :ref:`??? <src>`
   | **AoW:** 9 days (the rest)

   **Chapter outline:**

   * *RRR model, registrars*
   * *Registrations*
      * Registrable objects + relationships
      * Objects states, objects life cycle
      * Object sharing
      * Object history
   * Zones
      * *generation*
   * Logging :sup:`src:NOTES`
      * audit logging vs. process logging
         * explain difference, link to Admin/Config
   * Technical checks
      * *general info*
      * types :sup:`src:WIKI/Test`
   * Notifications & Reports
      * *general info*
      * (Mailing, Messaging...)
      * Delivery channels (email, sms, letters, poll msgs)
      * types  :sup:`src:DB`
         * (group by object type? or use table?)
         * Domain Expiration Warning
         * Domain Deletion Warning
         * ...expirations, validations :sup:`ENUM`, changes, ...
         * Tech.check results (go into poll messages + contact email?)
   * IDN support (we can register domains in UTF-8 and display them, but we can't restrict the character set just to a local alphabet)
      * *general info*
   * DNSSEC support (get keys from registrars + include them in zone file)
      * *general info*
   * ENUM
      * *general info*
   * Accounting (Pricing, Payments, Charging, Invoicing)
      * *general info*

   .. struct-end

The main goal of the FRED is to administer authoritative information
on domains, domain ownership and owners which is then distributed via the DNS
(zone file) as well as served in response to public queries (whois).
To accomplish this, the system allows to input the relevant information into
its database through the registration process and comprises the means
to administrate existing data.

The relevant information obtained by the registration process is grouped
into so-called **registrable objects**.

To ensure the authenticity of the data, only authorized entities (registrars)
can perform registrations and modify existing data in the Registry.

.. todo:: hard-coded and configurable rules

.. contents:: Chapter TOC
   :local:

.. include:: RRRModel.rst

.. include:: Genzone.rst

.. include:: EPPProtocol.rst

.. include:: Whois.rst

.. include:: Notifications.rst

.. include:: TecChecks.rst

.. include:: MultiLanguage.rst

.. include:: DNSSECSupport.rst

.. include:: InvoicingBanking.rst

.. include:: ENUM.rst

.. include:: ContactVerification.rst

.. include:: ObjectLocking.rst

.. include:: DomainNameRestrictions.rst
