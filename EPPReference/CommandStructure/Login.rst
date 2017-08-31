
.. index:: login

Login
=====

A login :ref:`command <struct-command>` is used to establish and authenticate
a session with the EPP server. The login command must be sent to the server
before any other EPP command and identifies and authenticates
the client identifier to be used by the session.

An EPP session is terminated by a :doc:`Logout` command.

The login command is a ``login`` element in the default namespace
(``urn:ietf:params:xml:ns:epp-1.0``).

.. index:: Ⓔlogin, ⒺclID, Ⓔpw, ⒺnewPW, Ⓔoptions, Ⓔversion, Ⓔlang, Ⓔsvcs,
   ⒺobjURI, ⒺsvcExtension, ⒺextURI

Command element structure
-------------------------

The ``<login>`` element contains the following child elements:

* ``<clID>`` **(1)** – the client identifier as :term:`eppcom:clIDType`,
* ``<pw>`` **(1)** – the client's plain-text password as :term:`epp:pwType`,
  case sensitive,
* ``<newPW>`` **(0..1)** – a new password to be used for subsequent login
  commands as :term:`epp:pwType`, case sensitive,
* ``<options>`` **(1)** – options of the EPP communication with the server:

   * ``<version>`` **(1)** – the protocol version to be used;
     this must be ``1.0``,
   * ``<lang>`` **(1)** – the response-text language to be used;
     this must be one of the values that are announced in :doc:`the greeting
     </EPPReference/ProtocolBasics/ServiceDiscovery>` (usually ``en`` or ``cs``),

* ``<svcs>`` **(1)** – list of services to be used during the session – declare
  the schemas for all the objects that will be manipulated during the session:

   * ``<objURI>`` **(1..n)** – an object namespace URI as :term:`xs:anyURI`.
     Further details on the namespace URIs can be found in the
     :doc:`/EPPReference/SchemasNamespaces/index` section.
   * ``<svcExtension>`` **(0..1)** – list of service extensions – declare
     the schema extensions for all the objects that will be manipulated during
     the session:

      * ``<extURI>`` **(1..n)** – an extension namespace URI as :term:`xs:anyURI`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <login>
            <clID>REG-MYREG</clID>
            <pw>passwd</pw>
            <options>
               <version>1.0</version>
               <lang>en</lang>
            </options>
            <svcs>
               <objURI>http://www.nic.cz/xml/epp/contact-1.6</objURI>
               <objURI>http://www.nic.cz/xml/epp/nsset-1.2</objURI>
               <objURI>http://www.nic.cz/xml/epp/domain-1.4</objURI>
               <objURI>http://www.nic.cz/xml/epp/keyset-1.3</objURI>
               <svcExtension>
                  <extURI>http://www.nic.cz/xml/epp/enumval-1.2</extURI>
               </svcExtension>
            </svcs>
         </login>
         <clTRID>sdmj001#17-03-06at18:48:03</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > login REG-MYREG passwd

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
