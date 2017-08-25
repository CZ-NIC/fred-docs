
.. index::
   pair: info; nsset

Info nsset
=============

A nsset info :ref:`command <struct-command>` is used to view details of a nsset.

The nsset info command is an ``info`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

The command must be contained in the ``<info>`` command class.

.. index:: Ⓔinfo, Ⓔid

Command element structure
-------------------------

The ``<nsset:check>`` element must declare the ``nsset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<nsset:id>`` **(1..n)**  – a nsset handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
      <info>
         <nsset:info xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.xsd">
            <nsset:id>NID-MYNSSET</nsset:id>
         </nsset:info>
      </info>
      <clTRID>kttq005#17-07-31at12:21:02</clTRID>
   </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > info_nsset NID-MYNSSET

.. index:: ⒺinfData, Ⓔid, Ⓔroid, Ⓔstatus,
   ⒺclID, ⒺcrID, ⒺcrDate, ⒺupID, ⒺupDate, ⒺtrDate, ⒺauthInfo,
   Ⓔns, Ⓔname, Ⓔaddr, Ⓔtech, Ⓔreportlevel,
   ⓐs, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

.. _nsset-infdata:

The response data element (``<resData>``) contains a single child element
``<nsset:infData>``  which declares the ``nsset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<nsset:id>`` **(1)** the nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:roid>`` **(1)** the nsset repository identifier as :term:`eppcom:roidType`,
* ``<nsset:status>`` **(0..6)** the :ref:`nsset object state(s) <mng-nsset-stat>`:
   * ``@s`` **(R)** – the state name as one of values:
      * ``ok``
      * ``linked``
      * ``serverDeleteProhibited``
      * ``serverTransferProhibited``
      * ``serverUpdateProhibited``
      * ``deleteCandidate``
   * ``@lang`` – the language of the state description as a :term:`xs:language` (default: ``en``),
   * element content: the state description as a :term:`xs:normalizedString`,
* ``<nsset:clID>`` **(1)** – the designated registrar handle as :term:`eppcom:clIDType`,
* ``<nsset:crID>`` **(0..1)** – the handle of the registrar who created this nsset as :term:`eppcom:clIDType`,
* ``<nsset:crDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`,
* ``<nsset:upID>`` **(0..1)** – the handle of the registrar who was the last to update this nsset as :term:`eppcom:clIDType`,
* ``<nsset:upDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last update as :term:`xs:dateTime`,
* ``<nsset:trDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last transfer as :term:`xs:dateTime`,
* ``<nsset:authInfo>`` **(0..1)** – authorization information (transfer password) as :term:`fredcom:authInfoType`,
* ``<nsset:ns>`` **(0..10)** – a nameserver given by:
   * ``<nsset:name>`` **(1)** – a nameserver hostname as :term:`eppcom:labelType`,
   * ``<nsset:addr>`` **(0..n)** – a namesever's IP address as :term:`nsset:addrStringType`,
* ``<nsset:tech>`` **(1..n)** – a technical contact handle as :term:`fredcom:objIDType`,
* ``<nsset:reportlevel>`` **(1)** – the report level of technical checks as :term:`nsset:reportlevelType`.

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
         <nsset:infData xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.1.xsd">
            <nsset:id>NID-MYNSSET</nsset:id>
            <nsset:roid>N0009907595-CZ</nsset:roid>
            <nsset:status s="linked">Has relation to other records in the registry</nsset:status>
            <nsset:clID>REG-MYREG</nsset:clID>
            <nsset:crID>REG-MYREG</nsset:crID>
            <nsset:crDate>2017-07-11T13:28:42+02:00</nsset:crDate>
            <nsset:upID>REG-MYREG</nsset:upID>
            <nsset:upDate>2017-07-27T16:54:53+02:00</nsset:upDate>
            <nsset:ns>
               <nsset:name>ns1.mydomain.cz</nsset:name>
               <nsset:addr>111.222.111.222</nsset:addr>
            </nsset:ns>
            <nsset:ns>
               <nsset:name>ns.otherdomain.cz</nsset:name>
            </nsset:ns>
            <nsset:tech>CID-TECH2</nsset:tech>
            <nsset:reportlevel>4</nsset:reportlevel>
         </nsset:infData>
      </resData>
      <trID>
         <clTRID>kttq005#17-07-31at12:21:02</clTRID>
         <svTRID>ReqID-0000140998</svTRID>
      </trID>
   </response>
   </epp>
