
.. index::
   pair: sendAuthInfo; contact
   triple: send; authInfo; contact

Send auth.info for contact
==========================

A contact sendAuthInfo command is used to provide the transfer password of a contact to the contact.

The client sends only the request for the provision to the Registry and
the Registry sends the password to the email of the contact.

This command is a part of the :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

The command must be contained in the ``<fred:sendAuthInfo>`` command type.

.. index:: Ⓔextcommand, ⒺsendAuthInfo, Ⓔid

Command element structure
-------------------------

The ``<contact:sendAuthInfo>`` element must declare the ``contact`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<contact:id>`` **(1)** – a contact handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <extension>
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.0.xsd">
         <!-- Custom command type -->
         <fred:sendAuthInfo>
            <!-- The object-defined command -->
            <contact:sendAuthInfo xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
               <contact:id>CID-MYOWN</contact:id>
            </contact:sendAuthInfo>
         </fred:sendAuthInfo>
         <fred:clTRID>rhgo002#17-08-08at17:10:00</fred:clTRID>
      </fred:extcommand>
   </extension>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > sendauthinfo_contact CID-MYOWN

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
