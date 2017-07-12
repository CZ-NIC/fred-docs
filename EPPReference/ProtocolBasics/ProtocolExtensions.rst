


FRED protocol extensions
========================

Protocol-level extensions are extensions in the XPath ``/epp/extension/*:*``.

The FRED EPP extends the protocol in such way that the ``<extension>`` element
*if used*, must contain only a single child:

* ``<fred:extcommand>`` **(1)** – container for extending commands which must declare
  the FRED namespace and schema and can contain **one of** the custom commands:
   * ``<fred:creditInfo/>`` – request information about the credit of the
     current client, see :doc:`../CommandStructure/CreditInfo`,
   * ``<fred:sendAuthInfo>`` – request a transfer password of an object,
     see :doc:`../CommandStructure/SendAuthInfo/index`,
   * ``<fred:test>`` – request a technical check,
     see :doc:`../CommandStructure/Test/index`,
   * or one of the listing commands, e.g. ``<fred:listDomains/>``,
     for the complete reference of listing commands see :doc:`../CommandStructure/List/index`.

  The custom command may be followed by the ``<fred:clTRID>`` element **(0..1)**
  (like the standard commands but from the ``fred`` namespace), which contains
  a client :ref:`transaction identifier <trans-ident>` as :term:`epp:trIDStringType`.



.. code-block:: xml
   :caption: Example of a protocol extension

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">

      <!-- Standard container for protocol extensions -->
      <extension>

      <!-- FRED's container for extending commands -->
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">

         <!-- An extending command (some have descendants) -->
         <fred:listDomains/>
         <!-- Transaction identification of the extending command -->
         <fred:clTRID>jqsi002#17-05-18at16:58:03</fred:clTRID>

      </fred:extcommand>

      </extension>

   </epp>

The examples of responses are illustrated for each specific command with its
structure description in further chapters.
