
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

.. todo:: hard-coded and configurable rules - maybe as Concept?
   :class: todo-backlog

.. contents:: Chapter TOC
   :local:
   :backlinks: none

.. _features-gen-rrrmodel:

.. include:: RRRModel.rst

.. _features-gen-genzone:

.. include:: Genzone.rst

.. _features-gen-epp:

.. include:: EPPProtocol.rst

.. _features-gen-whois:

.. include:: Whois.rst

.. _features-gen-gdpr:

.. include:: GDPRCompliance.rst

.. _features-gen-notifications:

.. include:: Notifications.rst

.. _features-gen-tecchecks:

.. include:: TecChecks.rst

.. _features-gen-multilang:

.. include:: MultiLanguage.rst

.. _features-gen-dnssec:

.. include:: DNSSECSupport.rst

.. _features-gen-billing:

.. include:: InvoicingBanking.rst

.. _features-gen-enum:

.. include:: ENUM.rst

.. _features-gen-contverif:

.. include:: ContactVerification.rst

.. _features-gen-contmerger:

.. include:: ContactMerger.rst

.. _features-gen-locks:

.. include:: ObjectLocking.rst

.. _features-gen-handleformat:

.. include:: DomainHandleValidation.rst

.. _features-gen-akm:

.. include:: AKM.rst

.. _features-gen-rs:

.. include:: RecordStatements.rst

.. _features-gen-auditlog:

.. include:: AuditLog.rst
