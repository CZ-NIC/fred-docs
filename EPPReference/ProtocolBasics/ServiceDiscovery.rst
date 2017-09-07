


Service discovery
=================

To request service information, the client sends a *hello* message and the server
replies with a *greeting* message which contains the service information.

The server also replies with a *greeting* when a TCP connection is initiated.

.. index:: hello, Ⓔhello

Hello element structure
-----------------------

The ``<hello/>`` element is a child of ``<epp>`` and is defined in the standard
EPP namespace.

The element must not contain any child elements nor attributes.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">

    <hello/>

   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > hello

.. index:: greeting, Ⓔgreeting

Greeting element structure
--------------------------

The ``<greeting>`` element is a child of ``<epp>`` and is defined in the standard
EPP namespace.

It contains the following child elements:

* ``<svID>`` – the name of the EPP server
  as a :term:`xs:normalizedString` of the length between 3 and 64 characters,
* ``<svDate>`` – the server's :ref:`timestamp <mngobj-timestamps>` as :term:`xs:dateTime`,
* ``<svcMenu>`` – services supported by the EPP server:

   * ``<version>`` **(1..n)** – listing of protocol versions supported by the server;
     the FRED EPP server supports only one version and that is ``1.0``,
   * ``<lang>`` **(1..n)** – listing of the available localizations of response texts;
     the FRED EPP server provides two localizations by default: ``en`` and ``cs``,
   * ``<objURI>`` **(1..n)** – listing of a :doc:`managed object <../ManagedObjects/index>`
     identified by its namespace as :term:`xs:anyURI`,
   * ``<svcExtension>`` **(0..1)** – a list of :ref:`command/response-level
     extensions <command-ext>` of objects supported by the server:

      * ``<extURI>`` **(1..n)** – an extension namespace as :term:`xs:anyURI`,

* ``<dcp>`` – data collection policy that describes the server's privacy policy
  for data collection and management:

   * ``<access>`` **(1)** – describes the access provided by the server
     to the client on behalf of the originating data source; must contain
     **one of** the following child elements:

      + ``<all/>`` – Access is given to all identified data.
      + ``<none/>`` – No access is provided to identified data.
      + ``<null/>`` – Data is not persistent, so no access is
        possible.
      + ``<personal/>`` – Access is given to identified data relating
        to individuals and organizational entities.
      + ``<personalAndOther/>`` – Access is given to identified data
        relating to individuals, organizational entities, and
        other data of a non-personal nature.
      + ``<other/>`` – Access is given to other identified data of
        a non-personal nature.

   * ``<statement>`` **(1..n)** – describe data collection purposes,
     data recipients, and data retention:

      * ``<purpose>`` **(1)** – describes the purposes for which data is
        collected; must contain **one or more of** the following child elements:

         + ``<admin/>`` – Administrative purposes.  Information can be
           used for administrative and technical support of the
           provisioning system.
         + ``<contact/>`` – Contact for marketing purposes.  Information
           can be used to contact individuals, through a communications
           channel other than the protocol, for the promotion of a product or service.
         + ``<prov/>`` – Object-provisioning purposes.  Information can
           be used to identify objects and inter-object
           relationships.
         + ``<other/>`` – Other purposes.  Information may be used in
           other ways not captured by the above definitions.

      * ``<recipient>`` **(1)** – describes the recipients of collected data;
        must contain **one or more of** the following child elements:

         + ``<other/>`` – Other entities following unknown practices.
         + ``<ours>`` – Server operator and/or entities acting as agents
           or entities for whom the server operator is acting as an
           agent.  An agent in this instance is defined as a third
           party that processes data only on behalf of the service
           provider for the completion of the stated purposes.  The
           ``<ours>`` element may contain a ``<recDesc>`` element **(0..1)**
           that can be used to describe the recipient.
         + ``<public/>`` – Public forums.
         + ``<same/>`` – Other entities following server practices.
         + ``<unrelated/>`` – Unrelated third parties.

      * ``<retention>`` **(1)** – describes data retention practices; must
        contain **one of** the following child elements:

         + ``<business/>`` – Data persists per business practices.
         + ``<indefinite/>`` – Data persists indefinitely.
         + ``<legal/>`` – Data persists per legal requirements.
         + ``<none/>`` – Data is not persistent and is not retained for
           more than a brief period of time necessary to make use of
           it during the course of a single online interaction.
         + ``<stated/>`` – Data persists to meet the stated purpose.

      * ``<expiry>`` **(0..1)** – describes the lifetime of the policy; must
        contain **one of** the following child elements:

         + ``<absolute/>`` – The policy is valid from the current date
           and time until it expires on the specified date and time.
         + ``<relative/>`` – The policy is valid from the current date
           and time until the end of the specified duration.

  More about DCP in :rfc:`5730#page-9`.

.. code-block:: xml
   :caption: Example

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
