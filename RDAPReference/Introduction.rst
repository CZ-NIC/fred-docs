


Introduction
------------

The Registration Data Access Protocol (RDAP) is built as a RESTful API
using the benefits of HTTP(S).

The RDAP standard allows only two HTTP methods: **HEAD** and **GET**.
More on usage of HTTP in :rfc:`7480`.

Client authentication is **not** implemented, all data in responses is public.

IDNs are fully supported (both A-labels and U-labels, :rfc:`5890#section-2.3.2.1`).

Registered RDAP servers can be found at https://data.iana.org/rdap/dns.json.

.. rubric:: Conformance of this reference

* RDAP Level 0
* FRED Extension Version 0

.. rubric:: Implemented interface overview

FRED RDAP does not implement any :dfn:`RIR (Regional Internet Registry)` functionality,
only some of :dfn:`DNR (Domain Name Registry)` functionality as follows:

* Lookup:
   * Domain by name (reverse lookup by IP not implemented)
   * Nameserver by hostname (reverse lookup by IP not implemented)
   * Entity by handle
* Unimplemented lookup: IP (\ ``/ip``), autonomous system (\ ``/as``)
* Lookup extensions:
   * FRED nsset by handle
   * FRED keyset by handle
* Help (\ ``/help``)
* Search queries are **not** implemented (\ ``/domains``, ``/nameservers``,
  ``/entities``)

.. rubric:: Specifications

* :rfc:`7480` HTTP Usage in the Registration Data Access Protocol (RDAP)
* :rfc:`7481` Security Services for the Registration Data Access Protocol (RDAP)
* :rfc:`7482` Registration Data Access Protocol (RDAP) Query Format
* :rfc:`7483` JSON Responses for the Registration Data Access Protocol (RDAP)
* :rfc:`7484` Finding the Authoritative Registration Data (RDAP) Service
* :rfc:`8056` Extensible Provisioning Protocol (EPP)
  and Registration Data Access Protocol (RDAP) Status Mapping
* `FRED RDAP Extension Specification <https://fred.nic.cz/rdap-extension/>`_
