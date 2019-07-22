


Version 2.39
==========================

Release 2.39.2
----------------

.. rubric:: Bugfixes

* Minor changes in packaging (client, pyfred, server, transproc, webadmin)
* IDL (Accounting): Add optional custom tax date to payment import
* Server: Fix default configuration



Release 2.39.1
-----------------

.. rubric:: Bugfixes

* Cdnskey-scanner: Prolong the time gap between DNS queries
* Database: Fix autoanalysis of ``contact`` and ``contact_address`` tables
* (:term:`CZ-specific`) Server (fred-mifd): Fix detection of changes in MojeID
  contact data (avoid dropping of verification states)
* Server: Fix logging in unix whois (IDN conversion error)



Release 2.39.0
----------------

.. rubric:: Enhancements

* all components: update LICENSEs to GPLv3+ (code) and CC BY-SA 4.0 (docs)
* Database: add UUID identifier for :term:`registrable object`\ s and their history records
* Libfred: a new component and repository that reimplements operations on core registry objects
* Server: remove an obsolete database layer from back end -- phase 2
* Daphne: allow administrative unblocking of a contact together with a domain if possible
* complete porting C++ components from Autotools to CMake -- affects
  :doc:`installation from sources </AdminManual/Installation/SourceTar>`
* continue porting Python components from Distutils to Setuptools (Client, WebAdmin)
* Client repository no longer contains compiled ``fred-client``,
  added README with build instructions
