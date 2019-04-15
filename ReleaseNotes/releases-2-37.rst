


Version 2.37
============

Release 2.37.3
--------------

.. rubric:: Bugfixes

* Doc2pdf: (\ :term:`CZ-specific`) fixed helios.xsl transformation (invoice export)



Release 2.37.2
--------------

.. rubric:: Bugfixes

* Database: restore (alter function schemas for security reasons)



Release 2.37.1
--------------

.. rubric:: Bugfixes

* Server: fixed sending of authinfo to multiple recipients when sending it to an email in the registry
* Server: fixed separator escaping in CSV serializer



Release 2.37.0
--------------

.. rubric:: Enhancements

* :term:`GDPR` compliance – dealing with personal information
   * EPP: server disclosure policy switched to *hide by default* (used to be *show by default*):
      * changed *greeting* content: ``dcp/access/all -> dcp/access/none``
      * ``contact:info`` response displays disclosure settings with ``flag="1"``
        (in reverse to previous versions)
      * affected also behaviour of ``contact:create`` and ``contact:update``
   * added new :term:`public request` types (requests for personal information)
     with a new web form, fred-admin procedure, filtering and resolving in Daphne,
     and an email template
   * provided utility ``fred-disclose-flags-update`` for a custom reset
     of contact disclosure preference
   * see also :doc:`Upgrade-2-37`

* DB: improved email template for contact identification (included phone number)
* WebWhois: removed some configuration options from the list of registrars (moved to CMS)
* removed old IDL types in pyfco (affects WebWhois, RDAP, Daphne)
* continuing preparations to port Python 2 code to Python 3

.. rubric:: Bugfixes

* Daphne: fixed returning zone access to a registrar from whom the access
  to this zone was taken away before
* EPPClient: fixed interpretation of disclose flags in responses to ``contact:info``
  to handle both the old and the new server disclosure policy
