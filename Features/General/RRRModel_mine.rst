

.. DNS requires an association of two or more nameservers (primary and backup)
   with a domain => nameserver set
   to enable the chain of trust in the DNS, a set of keys can be associated
   with a domain => key set
   why contacts -
   implements protocol for communication with registrars
   Thick regisrty - contains all whois information

Registry—Registrar—Registrant model
-----------------------------------

Potential domain owners (Registrants) may not be known to the Registry prior
to a registration and therefore the Registry has no means to authorize
their access to the database.

Therefore registrations and changes to existing information are made
by the Registrars which are organizations authorized by the Registry to request
registrations of domains and related operations over registrable objects.

Sponsoring Registrar
^^^^^^^^^^^^^^^^^^^^
Each registrable object in the Registry is managed by exactly one Registrar—the
sponsoring Registrar—and only this Registrar may modify it.

A Registrant is allowed to change the sponsoring Registrar of their registrable
object by means of a transfer process.

Registrable objects
-------------------

The registrable objects are the following:

* Domain,
* Contact (in roles of domain owners, administrative contacts or technical contacts),
* NSSet (a group of name servers), and
* KeySet (a group of DNSSEC keys).

Object relationships
^^^^^^^^^^^^^^^^^^^^

+ Object sharing

Object life cycle (states)
^^^^^^^^^^^^^^^^^^^^^^^^^^

Object history
^^^^^^^^^^^^^^


.. Operations & Prohibitions
   -------------------------
