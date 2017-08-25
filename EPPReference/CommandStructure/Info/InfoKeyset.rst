
.. index::
   pair: info; keyset

Info keyset
=============

A keyset info :ref:`command <struct-command>` is used to view details of a keyset.

The keyset info command is an ``info`` element in the ``keyset`` namespace
(``http://www.nic.cz/xml/epp/keyset-1.3``).

The command must be contained in the ``<info>`` command class.

.. index:: Ⓔinfo, Ⓔid

Command element structure
-------------------------

The ``<keyset:check>`` element must declare the ``keyset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<keyset:id>`` **(1..n)**  – a keyset handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <info>
            <keyset:info xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.xsd">
               <keyset:id>KID-MYKEYSET</keyset:id>
            </keyset:info>
         </info>
         <clTRID>gyyp005#17-07-31at13:03:07</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > info_keyset NID-MYNSSET

.. index:: ⒺinfData, Ⓔid, Ⓔroid, Ⓔstatus,
   ⒺclID, ⒺcrID, ⒺcrDate, ⒺupID, ⒺupDate, ⒺtrDate, ⒺauthInfo,
   Ⓔdnskey, Ⓔflags, Ⓔprotocol, Ⓔalg, ⒺpubKey, Ⓔtech,
   ⓐs, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

.. _keyset-infdata:

The response data element (``<resData>``) contains a single child element
``<keyset:infData>``  which declares the ``keyset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<keyset:id>`` **(1)** the keyset handle as :term:`fredcom:objIDType`,
* ``<keyset:roid>`` **(1)** the keyset repository identifier as :term:`eppcom:roidType`,
* ``<keyset:status>`` **(0..6)** the :ref:`keyset object state(s) <mng-keyset-stat>`:
   * ``@s`` **(R)** – the state name as one of values:
      * ``ok``
      * ``linked``
      * ``serverDeleteProhibited``
      * ``serverTransferProhibited``
      * ``serverUpdateProhibited``
      * ``deleteCandidate``
   * ``@lang`` – the language of the state description as a :term:`xs:language` (default: ``en``),
   * element content: the state description as a :term:`xs:normalizedString`,
* ``<keyset:clID>`` **(1)** – the designated registrar handle as :term:`eppcom:clIDType`,
* ``<keyset:crID>`` **(0..1)** – the handle of the registrar who created this keyset as :term:`eppcom:clIDType`,
* ``<keyset:crDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`,
* ``<keyset:upID>`` **(0..1)** – the handle of the registrar who was the last to update this keyset as :term:`eppcom:clIDType`,
* ``<keyset:upDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last update as :term:`xs:dateTime`,
* ``<keyset:trDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last transfer as :term:`xs:dateTime`,
* ``<keyset:authInfo>`` **(0..1)** – authorization information (transfer password) as :term:`fredcom:authInfoType`,
* ``<keyset:dnskey>`` **(0..10)** – a DNS key (:ref:`see object's attributes
  for allowed values <mng-keyset-attr>`) given by:
   * ``<keyset:flags>`` **(1)** – flags as :term:`xs:unsignedShort`,
   * ``<keyset:protocol>`` **(1)** – protocol as :term:`xs:unsignedByte`,
   * ``<keyset:alg>`` **(1)** – algorithm as :term:`xs:unsignedByte`,
   * ``<keyset:pubKey>`` **(1)** – public key as :term:`keyset:keyT`,
* ``<keyset:tech>`` **(1..n)** – a technical contact handle as :term:`fredcom:objIDType`.

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
            <keyset:infData xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.1.xsd">
               <keyset:id>KID-MYKEYSET</keyset:id>
               <keyset:roid>K0009907596-CZ</keyset:roid>
               <keyset:status s="linked">Has relation to other records in the registry</keyset:status>
               <keyset:clID>REG-MYREG</keyset:clID>
               <keyset:crID>REG-MYREG</keyset:crID>
               <keyset:crDate>2017-07-11T13:28:45+02:00</keyset:crDate>
               <keyset:upID>REG-MYREG</keyset:upID>
               <keyset:upDate>2017-07-20T20:04:35+02:00</keyset:upDate>
               <keyset:authInfo>aBcD234</keyset:authInfo>
               <keyset:dnskey>
                  <keyset:flags>257</keyset:flags>
                  <keyset:protocol>3</keyset:protocol>
                  <keyset:alg>5</keyset:alg>
                  <keyset:pubKey>aXN4Y2lpd2ZicWtkZHF4dnJyaHVtc3BreXN6ZGZy</keyset:pubKey>
               </keyset:dnskey>
               <keyset:dnskey>
                  <keyset:flags>257</keyset:flags>
                  <keyset:protocol>3</keyset:protocol>
                  <keyset:alg>5</keyset:alg>
                  <keyset:pubKey>eGVmbmZrY3lvcXFwamJ6aGt2YXhteXdkc2tjeXBp</keyset:pubKey>
               </keyset:dnskey>
               <keyset:tech>CID-TECH2</keyset:tech>
            </keyset:infData>
         </resData>
         <trID>
            <clTRID>gyyp005#17-07-31at13:03:07</clTRID>
            <svTRID>ReqID-0000141004</svTRID>
         </trID>
      </response>
   </epp>
