
.. _FRED-Features-Public:

Public features
===============

These are the features that the FRED public interface provides to the public.

.. only:: mode_structure

   .. struct-start

   **Sources:**  ? :ref:`??? <src>` | **AoW:** unplanned

   **Chapter outline:**

   * Anonymous end users
      * WebWhois, UnxWhois, RDAP
      * restrictions (CAPTCHA)
   * Registrants (Dom.Owners), Administrative contacts (Dom.),
     Technical contacts (NS/Keys)

      * Notifications? (see General features)
      * Validation of contact information
      * Registry object locking (blocking transfer/all changes)

   .. struct-end

.. contents::
   :local:
   :backlinks: none

Unix WHOIS
----------

* Domain lookup
* Contact lookup
* Nsset lookup
* Keyset lookup
* Registrar lookup
* Lookup by inverse keys:
   * domain:registrant
   * domain:admin-c
   * domain:temp-c
   * domain:nsset
   * domain:keyset
   * nsset:nserver
   * nsset:tech-c
   * keyset:tech-c
* Recursion on/off
* Lookup restriction by object types

Web WHOIS
---------

* Domain lookup
* Contact lookup
* Nsset lookup
* Keyset lookup
* Registrar lookup
* Associated objects are hyper-linked

RDAP
----

* Domain lookup
* Nameserver lookup
* Entity (contact) lookup
* Nsset lookup
* Keyset lookup

Public requests
---------------

* Request for sending authorization information
* Request for blocking object transfer / all changes
* Request for unblocking object transfer / all changes
* Request for sending personal info
* Requests (all of the above types) fullfilled to:
   * an email in the Registry are approved immediatelly and automatically
   * a custom email must be approved manually and accompanied by a confirmation:
      * Email signed with a digital certificate
      * Letter with a notarized signature

Registrar list
--------------

For each registrar:

* name,
* website,
* technologies (by interpreting registrar groups), :sup:`CZ-specific`
* certification, :sup:`CZ-specific`
* evaluation protocol, :sup:`CZ-specific`
* registration guide. :sup:`CZ-specific`

..
   Contact verification :sup:`CZ-specific`
   ---------------------------------------
