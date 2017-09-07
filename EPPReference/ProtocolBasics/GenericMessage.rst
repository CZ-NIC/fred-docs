


Generic message structure
=========================

This section describes the top-level syntax of the XML messages and explains
how it relates to various message types.

All messages must begin with an **XML prolog** to:

* identify the version of XML that is being used (`1.0 or 1.1
  <https://www.w3.org/TR/xml11/#sec-xml11>`_),
* identify the character encoding of the message (optional), and
* provide a hint to an XML parser that an external schema file is needed
  to validate the XML instance (optional).

.. code-block:: xml
   :caption: Example of XML prolog

   <?xml version="1.0" encoding="UTF-8" standalone="no"?>

.. TODO vyzkoušet, jestli server zvládne zpracovat jinou verzi XML
   a jiné kódování
   + doporučení co používat a co ne
   NOTE omezeno knihovnou libxml2
   NOTE vetsinu kodovani to zvladne, problem byl s GB...cosi, nejakymi asijskymi,
   evropska (Windows/IBM/ISO/UTF) to zvlada

.. Note::

   UTF-8 is the recommended and default character encoding for use with EPP.

   If the document requires an external definition
   (such as a schema) to be complete (for example to determine default values
   for absent optional attributes), then it is *not standalone*.

After the prolog, the **root element** follows and identifies the protocol and
its version. This is always ``<epp>`` in the standard base EPP namespace
(``urn:ietf:params:xml:ns:epp-1.0``) which must be declared at the ``<epp>``
element. See also :doc:`/EPPReference/SchemasNamespaces/index` on how to enable
client-side XML validation.

.. code-block:: xml
   :caption: Example of the root element

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp
      xmlns="urn:ietf:params:xml:ns:epp-1.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">

      <!-- message content -->

   </epp>

.. Note:: It is customary in the FRED and in the examples of this publication
   to declare this namespace as the default namespace (the one which does not
   have a prefix).

   A namespace can be used for the element, at which it was declared,
   and all its descendants and their attributes.
   `More on the scoping of namespaces.
   <https://www.w3.org/TR/REC-xml-names/#scoping-defaulting>`_



The singular child of the ``<epp>`` element determines the **type of a message**
and it must be **one of** the following:

* ``<hello>`` – service discovery request (contents and use described
  in :doc:`ServiceDiscovery`),
* ``<greeting>`` – service discovery reply (contents and use described
  in :doc:`ServiceDiscovery`),
* ``<command>`` – container for a standard EPP command (contents and use
  described in :doc:`Commands`),
* ``<response>`` – reply to a command (contents and use described
  in :doc:`Commands`),
* ``<extension>`` – protocol extension (non-standard request). The protocol
  extensions are described in :doc:`ProtocolExtensions`.



.. rubric:: Request-reply mapping of message types

The following table contains an illustration of relationships
between the message types to clarify which types are *requests* sent by a client
and which are *replies* sent by the server.

.. list-table::
   :header-rows: 1
   :widths: 30, 30, 40

   * - Service aspect
     - Request
     - Reply
   * - Service discovery
     - ``hello``
     - ``greeting``
   * - Commands
     - ``command``
     - ``response``
   * - Protocol extensions
     - ``extension``
     - ``response`` [*]_

.. [*] The content of a reply to a protocol extension is defined
   by the FRED EPP server as a standard response.

   All FRED protocol extensions are just commands, therefore having
   the standard response as a reply is sufficient.
