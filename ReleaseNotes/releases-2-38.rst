


Version 2.38
=============



Release 2.38.5
----------------

.. rubric:: Bugfixes

* AKM Client: fix insecured-domain key acceptance when interfered by a manually-added keyset



Release 2.38.4
----------------

.. rubric:: Bugfixes

* (\ :term:`CZ-specific`) Server (fred-mifd): fix MojeID PIN3 resending



Release 2.38.3
----------------

.. rubric:: Bugfixes

* (\ :term:`CZ-specific`) Stat collector: fix parsing of realms with asterisk
  in authority in MojeID stats



Release 2.38.2
-----------------

.. rubric:: Bugfixes

* fred-pain: Log suspicious invoices from FRED
* (\ :term:`CZ-specific`) Stat collector: query optimizations, add Py3 support
* Transproc: Restrict console logging to ERROR level
* WebWhois: Return status codes to HTML ``data-`` attributes of object details



Release 2.38.1
----------------

.. rubric:: Bugfixes

* Database:
   * fix ``mail_archive`` migration (modifies behaviour of the upgrade scripts
     ``2.32.0-2.33.0-{1,3,4}-*.sql``, see updated :doc:`./Upgrade-2-35`)
   * drop a constraint to allow multiple invoices for a single payment or
     a single invoice for multiple payments

     .. Important:: Run the upgrade script `2.35.0-2.35.1.sql
        <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.35.0-2.35.1.sql>`_,
        if you want to use :doc:`PAIN </Concepts/PAIN>` with FRED 2.38.

* Server (fred-accifd): fix search for a registrar by payment data
* Transproc: add another :term:`CZ-specific` bank connector



Release 2.38.0
----------------

.. rubric:: Enhancements

* Server (fred-admin): change ``--zone_ns_add`` syntax -- when entering
  multiple IP addresses, separate them with a space or repeat the argument
  (see :ref:`FRED-Admin-reginit-zone-ns`)
* Server: remove an obsolete database layer from back end
* Mod-eppd, Server (fred-rifd): make disclosure policy and default disclose flags
  configurable, see also :doc:`Upgrade-2-38`
* improve public requests -- asynchronous processing with a command in fred-admin
* continue porting to setuptools (``doc2pdf``, ``transproc``)
* continue porting to Python 3

* :term:`PAIN` :emphasis:`Phase 1` -- detach payment import and processing from FRED, |br|
  see also :doc:`/Concepts/PAIN` and :doc:`Upgrade-2-38`

   * new Django application ``django-pain``
      * ``fred-pain``: FRED plugin for PAIN
      * ``payments-pain``: Ginger plugin for PAIN (not released to the public)
   * IDL: new ``Accounting`` interface
   * Database: migrate ``bank_payment`` table to PAIN DB
   * Server:
      * fred-admin: remove ``--bank_import_xml`` command
      * new daemon ``fred-accifd`` will handle registrar credit based on payments already processed with PAIN
      * currently in transitional state - handles payment import call from PAIN because invoices are still managed with FRED
   * Transproc:
      * rename back-end command configuration variables
      * call ``django-pain`` instead of ``fred-admin``
   * WebAdmin:
      * remove ``Payments`` (move manual pairing to PAIN)
      * change format for saving search filters


.. rubric:: Bugfixes

* Server (fred-admin): check that a domain has not been deleted yet before deleting it
  (using the command ``--object_delete_candidates``
  with the argument ``--object_delete_spread_during_time``
  used to log an error when attempting to delete a domain repeatedly)
* Mod-eppd, Client: show extra-addr extension in the EPP greeting
  (``<extURI>http://www.nic.cz/xml/epp/extra-addr-1.0</extURI>``)
  when enabled in mod-eppd

   * Client upgrade is necessary!

* Server (fred-rifd): in ``sendauthinfo`` operations, check validity of the main email address
  of linked contacts; if there is no valid address in any of the linked contacts,
  end with the "2400 Command failed" error to signify that nothing will be sent
