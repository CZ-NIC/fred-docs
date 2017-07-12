
.. _FRED-EPPRef-XMLNS:

Schemas & namespaces
====================

.. todo:: add schemas

Standard namespaces
-------------------

* \urn:ietf:params:xml:ns:epp-1.0 – Extensible Provisioning Protocol v1.0
  – base protocol namespace (generic message structure), schema: ``epp-1.0.xsd``
* \urn:ietf:params:xml:ns:eppcom-1.0 – Extensible Provisioning Protocol v1.0
  shared structures, schema: ``eppcom-1.0.xsd``

Struktura XML dokumentů je
definována pomocí dvou XML schémat.
Namespace urn:ietf:params:xml:ns:epp-1.0 je definován základním schématem EPP.
Druhé schéma vedlejšího významu definuje namespace urn:ietf:params:xml:ns:eppcom-1.0
a jedná se o definici několika používaných jednoduchých datových typů,
u kterých se předpokládá, že budou sdíleny se schématy, které
EPP protokol rozšiřují. Jakékoliv úpravy EPP, které by znamenaly změnu těchto
dvou schémat, nejsou kompatibilní a protokol,
na nich postavený, nesmí být názvem EPP označován.

FRED-defined namespaces
-----------------------

* \http://www.nic.cz/xml/epp/fred-1.5 – protocol extensions (new commands), schema: :samp:`fred-1.5.{x}.xsd` vs. ``fred-1.5.xsd`` ???
* \http://www.nic.cz/xml/epp/fredcom-1.2 – protocol extension structures, schema: fredcom-1.2.x.xsd
* \http://www.nic.cz/xml/epp/domain-1.4 – Extension to Extensible Provisioning
  Protocol v1.0 domain – object extension, command-response mapping and data types
  for domains, schema: domain-1.4.x.xsd
* \http://www.nic.cz/xml/epp/contact-1.6 – Extension to Extensible Provisioning
  Protocol v1.0 contact provisioning – object extension and data types
  for contacts, schema: contact-1.6.x.xsd
* \http://www.nic.cz/xml/epp/nsset-1.2 – Extension to Extensible Provisioning
  Protocol v1.0 nameserver set provisioning – object extension and data
  types for nameserver sets, schema: nsset-1.2.x.xsd
* \http://www.nic.cz/xml/epp/keyset-1.3 – Extension to Extensible Provisioning
  Protocol v1.0 DNS-key set provisioning – object extension and data
  types for DNSSEC-key sets, schema: keyset-1.3.x.xsd
* \http://www.nic.cz/xml/epp/enumval-1.2 – extension for properties related
  to ENUM domain validation, schema: enumval-1.2.x.xsd

.. Note:: Documentation does not include elements that are deprecated.
