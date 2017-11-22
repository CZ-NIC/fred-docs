
.. index::
   pair: create; nsset

Create nsset
==============

A nsset create :ref:`command <struct-command>` is used to register a new nsset.

The nsset create command is a ``create`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

The command must be contained in the ``<create>`` command type.

.. index:: Ⓔcreate, Ⓔid, Ⓔns, Ⓔname, Ⓔaddr, Ⓔtech,
   ⒺauthInfo, Ⓔreportlevel

Command element structure
-------------------------

The ``<nsset:create>`` element must declare the ``nsset`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and it must contain the following child elements:

* ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDCreateType`.
* ``<nsset:ns>`` **(1..10)** – a nameserver given by:
   * ``<nsset:name>`` **(1)** – the nameserver hostname as :term:`eppcom:labelType`,
   * ``<nsset:addr>`` **(0..n)** – the namesever's IP address(es) as :term:`nsset:addrStringType`,
* ``<nsset:tech>`` **(1..10)** –  a handle of a contact that will be assigned
  as a technical contact as :term:`fredcom:objIDType`,
* ``<nsset:authInfo>`` **(0..1)** – authorization information (transfer password)
  as :term:`fredcom:authInfoType`; if omitted, the password will be generated
  by the server,
* ``<nsset:reportlevel>`` **(0..1)** – the default highest level of technical checks
  to be performed as :term:`nsset:reportlevelType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <create>
            <nsset:create xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.2.xsd">
               <nsset:id>NID-ANSSET</nsset:id>
               <nsset:ns>
                  <nsset:name>ns1.domain.cz</nsset:name>
               </nsset:ns>
               <nsset:ns>
                  <nsset:name>ns2.domain.cz</nsset:name>
               </nsset:ns>
               <nsset:ns>
                  <nsset:name>ns.indomain.cz</nsset:name>
                  <nsset:addr>217.31.207.130</nsset:addr>
                  <nsset:addr>217.31.207.131</nsset:addr>
               </nsset:ns>
               <nsset:tech>CID-TECH1</nsset:tech>
               <nsset:reportlevel>1</nsset:reportlevel>
            </nsset:create>
         </create>
         <clTRID>pvlt002#17-08-09at15:52:40</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > create_nsset NID-ANSSET ((ns1.domain.cz), (ns2.domain.cz), (ns.indomain.cz (217.31.207.130, 217.31.207.131))) CID-TECH1 NULL 1

.. index:: ⒺcreData, Ⓔid, ⒺcrDate

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data, and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<nsset:creData>``  which declares the ``nsset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`,
and it contains the following child elements:

* ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:crDate>`` **(1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`.

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
            <nsset:creData xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.2.xsd">
               <nsset:id>NID-ANSSET</nsset:id>
               <nsset:crDate>2017-08-09T15:53:15+02:00</nsset:crDate>
            </nsset:creData>
         </resData>
         <trID>
            <clTRID>pvlt002#17-08-09at15:52:40</clTRID>
            <svTRID>ReqID-0000141092</svTRID>
         </trID>
      </response>
   </epp>
