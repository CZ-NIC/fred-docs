
.. index::
   pair: info; domain

Info domain
===========

A domain info :ref:`command <struct-command>` is used to view details of a domain.

The domain info command is an ``info`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

The command must be contained in the ``<info>`` command type.

.. index:: Ⓔinfo, Ⓔname

Command element structure
-------------------------

The ``<domain:info>`` element must declare the ``domain`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<domain:name>`` **(1)**  – a domain name as :term:`eppcom:labelType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <info>
            <domain:info xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>mydomain.cz</domain:name>
            </domain:info>
         </info>
         <clTRID>iops002#17-07-28at13:14:47</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > info_domain mydomain.cz


.. index:: ⒺinfData, Ⓔname, Ⓔroid, Ⓔstatus,
   Ⓔregistrant, Ⓔadmin, Ⓔnsset, Ⓔkeyset, ⒺexDate,
   ⒺclID, ⒺcrID, ⒺcrDate, ⒺupID, ⒺupDate, ⒺtrDate, ⒺauthInfo,
   Ⓔtempcontact, ⓐs, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data, and transaction identification.

See also :ref:`succ-fail`.

.. _domain-infdata:

The response data element (``<resData>``) contains a single child element
``<domain:infData>``  which declares the ``domain`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<domain:name>`` **(1)** – the domain name as :term:`eppcom:labelType`,
* ``<domain:roid>`` **(1)** – the domain repository identifier as :term:`eppcom:roidType`,
* ``<domain:status>`` **(1..n)** – the :ref:`domain object state(s) <mng-domain-stat>`:
   * ``@s`` **(R)** – the state name as one of values:
      * ``ok``
      * ``serverDeleteProhibited``
      * ``serverRenewProhibited``
      * ``serverTransferProhibited``
      * ``serverUpdateProhibited``
      * ``serverRegistrantChangeProhibited``
      * ``serverBlocked``
      * ``serverOutzoneManual``
      * ``serverInzoneManual``
      * ``expired``
      * ``outzone``
      * ``notValidated`` :sup:`ENUM only`
      * ``deleteCandidate``
   * ``@lang`` – the language of the state description as a :term:`xs:language` (default: ``en``),
   * element content: the state description as a :term:`xs:normalizedString`,
* ``<domain:registrant>`` **(0..1)** – the domain owner handle as :term:`fredcom:objIDType`,
* ``<domain:admin>`` **(0..n)** – an administrative contact handle as :term:`fredcom:objIDType`,
* ``<domain:nsset>`` **(0..1)** – the nsset handle as :term:`eppcom:labelType`,
* ``<domain:keyset>`` **(0..1)** – the keyset handle as :term:`eppcom:labelType`,
* ``<domain:clID>`` **(1)** – the designated registrar's handle as :term:`eppcom:clIDType`,
* ``<domain:crID>`` **(0..1)** – the handle of the registrar who created this domain as :term:`eppcom:clIDType`,
* ``<domain:crDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`,
* ``<domain:upID>`` **(0..1)** – the handle of the registrar who was the last
  to update this domain as :term:`eppcom:clIDType`,
* ``<domain:upDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last update as :term:`xs:dateTime`,
* ``<domain:exDate>`` **(0..1)** – the date of expiration as :term:`xs:date`,
* ``<domain:trDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last transfer as :term:`xs:dateTime`,
* ``<domain:authInfo>`` **(0..1)** – authorization information (transfer password) as :term:`fredcom:authInfoType`,
* ``<domain:tempcontact>`` **(0..n)** – a temporary contact handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <response>
      <result code="1000">
         <msg>Command completed successfully</msg>
      </result>
      <resData>
         <domain:infData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
            <domain:name>mydomain.cz</domain:name>
            <domain:roid>D0009907597-CZ</domain:roid>
            <domain:status s="ok">Object is without restrictions</domain:status>
            <domain:registrant>CID-MYOWN</domain:registrant>
            <domain:admin>CID-ADMIN2</domain:admin>
            <domain:nsset>NID-MYNSSET</domain:nsset>
            <domain:clID>REG-MYREG</domain:clID>
            <domain:crID>REG-MYREG</domain:crID>
            <domain:crDate>2017-07-11T13:28:48+02:00</domain:crDate>
            <domain:upID>REG-MYREG</domain:upID>
            <domain:upDate>2017-07-18T10:46:19+02:00</domain:upDate>
            <domain:exDate>2020-07-11</domain:exDate>
            <domain:authInfo>rvBcaTVq</domain:authInfo>
         </domain:infData>
      </resData>
      <trID>
         <clTRID>iops002#17-07-28at13:14:47</clTRID>
         <svTRID>ReqID-0000140984</svTRID>
      </trID>
   </response>
   </epp>

ENUM extension
^^^^^^^^^^^^^^
The ``<domain:infData>`` element is used in the same way as described above.

The :ref:`response extension <response-ext>` is used to display the validation
of an ENUM domain and/or its publish flag.

The response's ``<extension>`` element contains a **single** ``<enumval:infData>``
element which declares the ``enumval`` namespace (``http://www.nic.cz/xml/epp/enumval-1.2``)
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and contains:

* ``<enumval:valExDate>`` **(0..1)**  – the validation expiration date as :term:`xs:date`,

* ``<enumval:publish>`` **(0..1)** – the setting for publishing the ENUM
  domain in a public directory as :term:`xs:boolean`; ``true`` – display, ``false`` – hide.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1000">
            <msg>Command completed successfully</msg>
         </result>
         <resData>
            <domain:infData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</domain:name>
               <domain:roid>D0009907598-CZ</domain:roid>
               <domain:status s="ok">Object is without restrictions</domain:status>
               <domain:registrant>CID-MYOWN</domain:registrant>
               <domain:admin>CID-ADMIN1</domain:admin>
               <domain:admin>CID-ADMIN2</domain:admin>
               <domain:nsset>NID-MYNSSET</domain:nsset>
               <domain:keyset>KID-MYKEYSET</domain:keyset>
               <domain:clID>REG-MYREG</domain:clID>
               <domain:crID>REG-MYREG</domain:crID>
               <domain:crDate>2017-07-14T16:22:32+02:00</domain:crDate>
               <domain:upID>REG-MYREG</domain:upID>
               <domain:upDate>2017-07-18T10:49:43+02:00</domain:upDate>
               <domain:exDate>2021-07-14</domain:exDate>
               <domain:authInfo>c8n9hraq</domain:authInfo>
            </domain:infData>
         </resData>
         <extension>
            <enumval:infData xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.0.xsd">
               <enumval:valExDate>2018-01-02</enumval:valExDate>
               <enumval:publish>0</enumval:publish>
            </enumval:infData>
         </extension>
         <trID>
            <clTRID>ites005#17-07-31at10:26:32</clTRID>
            <svTRID>ReqID-0000140992</svTRID>
         </trID>
      </response>
   </epp>
