
.. index::
   pair: create; keyset

Create keyset
==============

A keyset create :ref:`command <struct-command>` is used to register a new keyset.

The keyset create command is a ``create`` element in the ``keyset`` namespace
(``http://www.nic.cz/xml/epp/keyset-1.3``).

The command must be contained in the ``<create>`` command type.

.. index:: Ⓔcreate, Ⓔid, Ⓔdnskey, Ⓔflags, Ⓔprotocol,
   Ⓔalg, ⒺpubKey, Ⓔtech, ⒺauthInfo

Command element structure
-------------------------

The ``<keyset:create>`` element must declare the ``keyset`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and it must contain the following child elements:

* ``<keyset:id>`` **(1)** – the keyset handle as :term:`fredcom:objIDCreateType`.
* ``<keyset:dnskey>`` **(1..10)** – a DNS key (:ref:`see object's attributes
  for allowed values <mng-keyset-attr>`) given by:

   * ``<keyset:flags>`` **(1)** – flags as :term:`xs:unsignedShort`,
   * ``<keyset:protocol>`` **(1)** – protocol as :term:`xs:unsignedByte`,
   * ``<keyset:alg>`` **(1)** – algorithm as :term:`xs:unsignedByte`,
   * ``<keyset:pubKey>`` **(1)** – public key as :term:`keyset:keyT`,
* ``<keyset:tech>`` **(1..10)** –  a handle of a contact that will be assigned
  as a technical contact as :term:`fredcom:objIDType`,
* ``<keyset:authInfo>`` **(0..1)** – authorization information (transfer password)
  as :term:`fredcom:authInfoType`; if omitted, the password will be generated
  by the server.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <create>
            <keyset:create xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.2.xsd">
               <keyset:id>KID-AKEYSET</keyset:id>
               <keyset:dnskey>
                  <keyset:flags>257</keyset:flags>
                  <keyset:protocol>3</keyset:protocol>
                  <keyset:alg>5</keyset:alg>
                  <keyset:pubKey>AwEAAddt2AkLfYGKgiEZB5SmIF8EvrjxNMH6HtxWEA4RJ9Ao6LCWheg8</keyset:pubKey>
               </keyset:dnskey>
               <keyset:dnskey>
                  <keyset:flags>257</keyset:flags>
                  <keyset:protocol>3</keyset:protocol>
                  <keyset:alg>5</keyset:alg>
                  <keyset:pubKey>AwEAAddt2AkLfYGKgiEZB5SmIF8EvrjxNMH6HtxWEA4RJ9Ao6LCWheg9</keyset:pubKey>
               </keyset:dnskey>
               <keyset:tech>CID-TECH2</keyset:tech>
            </keyset:create>
         </create>
         <clTRID>dsce002#17-08-09at16:13:30</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > create_keyset KID-AKEYSET ((257 3 5 AwEAAddt2AkLfYGKgiEZB5SmIF8EvrjxNMH6HtxWEA4RJ9Ao6LCWheg8), (257 3 5 AwEAAddt2AkLfYGKgiEZB5SmIF8EvrjxNMH6HtxWEA4RJ9Ao6LCWheg9)) () CID-TECH2

.. index:: ⒺcreData, Ⓔid, ⒺcrDate

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data, and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<keyset:creData>``  which declares the ``keyset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`,
and it contains the following child elements:

* ``<keyset:id>`` **(1)** – the keyset handle as :term:`fredcom:objIDType`,
* ``<keyset:crDate>`` **(1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`.

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
            <keyset:creData xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.2.xsd">
               <keyset:id>KID-AKEYSET</keyset:id>
               <keyset:crDate>2017-08-09T16:13:50+02:00</keyset:crDate>
            </keyset:creData>
         </resData>
         <trID>
            <clTRID>dsce002#17-08-09at16:13:30</clTRID>
            <svTRID>ReqID-0000141095</svTRID>
         </trID>
      </response>
   </epp>
