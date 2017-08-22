
.. _FRED-EPPRef-XMLNS:

Namespaces & schemas
====================

.. todo:: This segment still has to undergo a review by a SME (fact-checking and proof-reading).

A namespace must be identified for each prefix using the :samp:`@xmlns:{prefix}` attribute.

.. Important:: The client must use the same version of a namespace as the server!
   The current namespace versions are listed in the ``greeting``
   (see :doc:`/EPPReference/ProtocolBasics/ServiceDiscovery`).

To enable XML validation on the client side, depending on the selected
XML-validation tool, there are 2 options:

* to link a namespace to the location of a schema (see the table below)
  inside messages using the ``@xsi:schemaLocation`` attribute,
  for the tool to locate the schema from here – *this option is illustrated
  in structure descriptions*, or
* to pass the location of the global schema as an argument
  to the XML-validation tool directly, such as:

  .. code-block:: shell

     xmllint --noout --schema "/usr/share/fred-client/schemas/all.xsd" -

The FRED EPP server as such does NOT require schema locations inside messages
and ignores them if they are present.

The global schema ``all-2.3.2.xsd`` (alias ``all.xsd``) imports the following partial schemas and
thus provides the definitions of all namespaces in a single file.

..
   tabularcolumns:: |p{0.075\textwidth}|p{0.25\textwidth}|p{0.575\textwidth}|

.. list-table:: Namespaces & schemas
   :header-rows: 1
   :widths: 25, 15, 60

   * - Namespace identifier
     - Schema file (partial)
     - Description
   * - ``urn:ietf:params:xml:ns:epp-1.0``
     - ``epp-1.0.xsd``
     - Extensible Provisioning Protocol v1.0 – protocol base (generic message structure)
   * - ``urn:ietf:params:xml:ns:eppcom-1.0``
     - ``eppcom-1.0.xsd``
     - Extensible Provisioning Protocol v1.0 – shared structures
   * - ``http://www.nic.cz/xml/epp/fred-1.5``
     - :samp:`fred-1.5.0.xsd`
     - FRED protocol extensions
   * - ``http://www.nic.cz/xml/epp/fredcom-1.2``
     - :samp:`fredcom-1.2.1.xsd`
     - FRED protocol extensions – shared structures
   * - ``http://www.nic.cz/xml/epp/domain-1.4``
     - :samp:`domain-1.4.2.xsd`
     - FRED object extension for domain provisioning – command-response mapping and structures
   * - ``http://www.nic.cz/xml/epp/contact-1.6``
     - :samp:`contact-1.6.2.xsd`
     - FRED object extension for contact provisioning – command-response mapping and structures
   * - ``http://www.nic.cz/xml/epp/nsset-1.2``
     - :samp:`nsset-1.2.2.xsd`
     - FRED object extension for nsset provisioning – command-response mapping and structures
   * - ``http://www.nic.cz/xml/epp/keyset-1.3``
     - :samp:`keyset-1.3.2.xsd`
     - FRED object extension for keyset provisioning – command-response mapping and structures
   * - ``http://www.nic.cz/xml/epp/enumval-1.2``
     - :samp:`enumval-1.2.0.xsd`
     - FRED command/response extensions for ENUM domains
   * - ``http://www.w3.org/2001/XMLSchema-instance``
     - N/A
     - Namespace for the XML Schema instance (``xsi`` prefix) |br|
       Required when the ``@xsi:schemaLocation`` attribute is used.
