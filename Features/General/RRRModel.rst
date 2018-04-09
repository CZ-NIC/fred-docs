


Registry–Registrar–Registrant model
-----------------------------------

The most important feature of the FRED is its database structured according
to the Registry–Registrar–Registrant model. Registrars communicate
with the Registry on behalf of registrants (domain owners).

Strong ownership model ensures that each registrable object in the database
is owned by one registrar (called the "designated registrar") and no other
registrar [#]_ may modify it.

A registrant is allowed to change the designated registrar of an object by means
of the :doc:`transfer process </Concepts/Transfer>`.

The registrable objects are the following:

* domain (regular or ENUM),
* contact (in roles of domain owners, administrative contacts
  or technical contacts),
* nsset (a group of name servers), and
* keyset (a group of DNSSEC keys).

All registration requests are resolved immediately if the requested object
is free.

The history of all changes regarding any object is accessible
through an administration interface.

Objects can be shared, i.e. one contact can be used multiple times
with domains, nssets or keysets. Similarly, one nsset or keyset can be linked
to several domains.

.. [#]
   With the exception of the system registrar which is
   used by the Registry to maintain the objects. The system registrar can modify
   all objects without limitation.
