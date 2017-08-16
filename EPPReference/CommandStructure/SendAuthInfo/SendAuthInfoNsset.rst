
.. index::
   pair: sendAuthInfo; nsset
   triple: send; authInfo; nsset

Send auth.info for nsset
==========================

A nsset sendAuthInfo command is used to provide the transfer password of a nsset
to the technical contacts of the nsset.

The client sends only the request for the provision to the Registry and
the Registry sends the password to the email of all technical contacts.

This command is a :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

The command must be contained in the ``fred:sendAuthInfo`` command class.

.. index:: Ⓔextcommand, ⒺsendAuthInfo, Ⓔid

Command element structure
-------------------------

The ``<nsset:sendAuthInfo>`` element must declare the ``nsset`` namespace
and schema and it must contain the following child elements:

* ``<nsset:id>`` **(1)** – a nsset handle as :term:`fredcom:objIDType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <extension>
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">
         <!-- Custom command class -->
         <fred:sendAuthInfo>
            <!-- The object-defined command -->
            <nsset:sendAuthInfo xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.xsd">
               <nsset:id>NID-MYNSSET</nsset:id>
            </nsset:sendAuthInfo>
         </fred:sendAuthInfo>
         <fred:clTRID>rhgo003#17-08-08at17:13:13</fred:clTRID>
      </fred:extcommand>
   </extension>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > sendauthinfo_nsset NID-MYNSSET

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
