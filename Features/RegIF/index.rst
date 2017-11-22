


Registrar features
==================

.. only:: mode_structure

   .. struct-start

   **Sources:**  ? :ref:`??? <src>` | **AoW:** unplanned

   **Chapter outline:**

   * EPP protocol features (standard)
      * check/create/delete... domain/contact
      * request authinfo, request tech.test (a part of std.EPP)
      * Poll messages (a part of std.EPP)
      * change registrar info? (a part of std.EPP???)
   * extended
      * check/create/delete... keyset/nsset

   .. struct-end

These are the features that the FRED EPP server provides to registrars.

They are common to both the FRED-client command-line interface and the API library.
The FRED-client has some :ref:`extra features <fred-client-extras>` of its own
in addition to the raw EPP service.

General requests
-------------------

* Discover the service
* Login into a session
* Logout from the session
* Get info about credit
* Read and discard poll notifications
* List objects in management

Manage domains
--------------

* Check availability of a domain
* Create a domain
* Get info about a domain
* Delete a domain
* Renew a domain
* Transfer a domain
* Update a domain
* Send authorization information of a domain to emails of the contacts linked with the domain

Manage contacts
---------------

* Check availability of a contact
* Create a contact
* Get info about a contact
* Delete a contact
* Transfer a contact
* Update a contact
* Send authorization information of a contact to emails of the contact

Manage nssets
--------------

* Check availability of a nsset
* Create a nsset
* Get info about a nsset
* Delete a nsset
* Transfer a nsset
* Update a nsset
* Request a technical check of a nsset
* Send authorization information of a nsset to emails of the contacts linked with the nsset

Manage keysets
--------------

* Check availability of a keyset
* Create a keyset
* Get info about a keyset
* Delete a keyset
* Transfer a keyset
* Update a keyset
* Send authorization information of a keyset to emails of the contacts linked with the keyset

.. _fred-client-extras:

FRED-client extras
------------------

* Command help
* Interactive input of commands
* Session settings (language, poll auto-acknowledgement)
* Debugging tools (verbosity, XML validation)
* Fetch from info
