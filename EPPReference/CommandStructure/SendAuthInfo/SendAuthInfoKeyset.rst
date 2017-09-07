
.. index::
   pair: sendAuthInfo; keyset
   triple: send; authInfo; keyset

Send auth.info for keyset
==========================

A keyset sendAuthInfo command is used to provide the transfer password of a keyset
to the technical contacts of the keyset.

The client sends only the request for the provision to the Registry and
the Registry sends the password to the email of all technical contacts.

This command is a part of the :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

The command must be contained in the ``<fred:sendAuthInfo>`` command type.

.. index:: Ⓔextcommand, ⒺsendAuthInfo, Ⓔid

Command element structure
-------------------------

The ``<keyset:sendAuthInfo>`` element must declare the ``keyset`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<keyset:id>`` **(1)** – a keyset handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <extension>
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">
         <!-- Custom command type -->
         <fred:sendAuthInfo>
            <!-- The object-defined command -->
            <keyset:sendAuthInfo xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.xsd">
               <keyset:id>KID-MYKEYSET</keyset:id>
            </keyset:sendAuthInfo>
         </fred:sendAuthInfo>
         <fred:clTRID>nuhe002#17-08-08at17:20:11</fred:clTRID>
      </fred:extcommand>
   </extension>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > sendauthinfo_keyset KID-MYKEYSET

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
