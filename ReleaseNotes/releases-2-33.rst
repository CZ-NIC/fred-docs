


Release 2.33.1
=========================

.. rubric:: Enhancements

* updated ``getdns`` (to v1.2.1) in cdnskey-scanner
* added mailing address handling to fred-client commands

.. rubric:: Bugfixes

* corrected ``serverBlocked`` description in db
* fixed error with null-byte-terminated public keys in cdnskey-scanner
* fixed ``info_contact`` mailing address response extension in EPP (omit ``sp`` element completely when empty)
* hotfix for EPP ``info_contact`` error when contact is ``serverBlocked``
