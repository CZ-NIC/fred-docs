
.. index::
   pair: sendAuthInfo; domain
   triple: send; authInfo; domain

Send auth.info for domain
=========================

A domain sendAuthInfo command is used to provide the transfer password
of a domain to the registrant and the administrative contacts of the domain.

The client sends only the request for the provision to the Registry and
the Registry sends the password to the email of the registrant and
of all administrative contacts.

This command is a :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

The command must be contained in the ``fred:sendAuthInfo`` command class.

.. index:: Ⓔextcommand, ⒺsendAuthInfo, Ⓔname

Command element structure
-------------------------

The ``<domain:sendAuthInfo>`` element must declare the ``domain`` namespace
and schema and it must contain the following child elements:

* ``<domain:name>`` **(1)**  – a domain name as :term:`eppcom:labelType`.

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
               <domain:sendAuthInfo xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
                  <domain:name>mydomain.cz</domain:name>
               </domain:sendAuthInfo>
            </fred:sendAuthInfo>
            <fred:clTRID>chsu002#17-08-08at16:33:10</fred:clTRID>
         </fred:extcommand>
      </extension>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > sendauthinfo_domain mydomain.cz

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
