


Service discovery
=================

To request service information, the client sends a *hello* message and the server
replies with a *greeting* message which contains the service information.

The server also replies with a *greeting* when a TCP connection is initiated.

.. index:: hello

Hello element structure
-----------------------

.. index:: Ⓔhello

The ``<hello/>`` element is a child of ``<epp>`` and defined in the standard
EPP namespace.

The element must not contain any child elements nor attributes.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">

    <hello/>

   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > hello

.. index:: greeting

Greeting element structure
--------------------------

.. index:: Ⓔgreeting

The ``<greeting>`` element is a child of ``<epp>`` and defined in the standard
EPP namespace.

It contains the following child elements:

* ``<svID>`` – the name of the EPP server
  as a :term:`xs:normalizedString` of the length between 3 and 64 characters,
* ``<svDate>`` – the server's current date and time in UTC as :term:`xs:dateTime`,
* ``<svcMenu>`` – services supported by the EPP server:
   * ``<version>`` **(1..n)** – listing of protocol versions supported by the server;
     the FRED EPP server supports only one version and that is ``1.0``,
   * ``<lang>`` **(1..n)** – listing of the available localizations of response texts;
     the FRED EPP server provides two localizations by default: ``en`` and ``cs``,
   * ``<objURI>`` **(1..n)** – listing of a :doc:`managed object <ManagedObjects>`
     identified by its namespace as :term:`xs:anyURI`,
   * ``<svcExtension>`` **(0..1)** – a list of :ref:`command/response-level
     extensions <command-ext>` of objects supported by the server:
      ``<extURI>`` **(1..n)** – an extension namespace as :term:`xs:anyURI`,
* ``<dcp>`` – data collection policy that describes the server's privacy policy
  for data collection and management:
   * ``<access>`` **(1)**
      * ``<all/>`` **(1)** – Clients are given access to all data.
   * ``<statement>`` **(1..n)**
      * ``<purpose>`` **(1)**
         * ``<admin/>`` **(0..1)** – The server collects data for administrative
           and technical support of the provisioning system.
         * ``<prov/>`` **(0..1)** – The server collects data to identify objects
           and inter-object relationships.
      * ``<recipient>`` **(1)**
         * ``<public/>`` **(1)** – The collected data is intended for public forums.
      * ``<retention>`` **(1)**
         * ``<stated/>`` **(1)** – The server retains data to meet the stated purpose.
  More about DCP in :rfc:`5730#page-9`.

.. Note:: The contents of a ``<greeting>`` from the FRED EPP server are fixed.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">

       <greeting>
           <svID>EPP server (DSDng)</svID>
           <svDate>2017-05-12T17:01:11+02:00</svDate>
           <svcMenu>
               <version>1.0</version>
               <lang>en</lang>
               <lang>cs</lang>
               <objURI>http://www.nic.cz/xml/epp/contact-1.6</objURI>
               <objURI>http://www.nic.cz/xml/epp/domain-1.4</objURI>
               <objURI>http://www.nic.cz/xml/epp/nsset-1.2</objURI>
               <objURI>http://www.nic.cz/xml/epp/keyset-1.3</objURI>
               <svcExtension>
                   <extURI>http://www.nic.cz/xml/epp/enumval-1.2</extURI>
               </svcExtension>
           </svcMenu>
           <dcp>
               <access>
                   <all/>
               </access>
               <statement>
                   <purpose>
                       <admin/>
                       <prov/>
                   </purpose>
                   <recipient>
                       <public/>
                   </recipient>
                   <retention>
                       <stated/>
                   </retention>
               </statement>
           </dcp>
       </greeting>

   </epp>
