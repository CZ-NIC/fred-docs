
.. _FRED-Features-Admin-CLI:

CLI admin features
-------------------

Manage zones
^^^^^^^^^^^^

* Create a zone
* Assign name servers to a zone
* Generate zone files (periodical)

Manage registrars
^^^^^^^^^^^^^^^^^

* List all registrars
* Add a registrar
* Set registrar's authentication data
* Grant a registrar access to a zone
* Include a registrar in a group of registrars
* Record registrar's certification
* Create a group of registrars
* Block a registrar
* Unblock a registrar
* Block registrars over request-usage limit (periodical)

Manage objects
^^^^^^^^^^^^^^

* Keep object states up-to-date and users notified about important events (periodical)
* Remove expired and inactive objects (periodical)
* Remind contacts to review their contact details (periodical)
* Merge a pair of duplicate contacts (manual)
* Merge a set of duplicate contacts (automatic)
* Update DNSSEC keys from CDNSKEY records (AKM) (periodical)
* Re-register a domain for another owner and force the domain expired

Manage finance
^^^^^^^^^^^^^^

* Set a price for an operation (with temporal validity)
* Set invoice numbering
* Import payments and attempt pairing (periodical)
* Assign credit to a registrar and create an invoice
* Generate poll messages about request usage (periodical)
