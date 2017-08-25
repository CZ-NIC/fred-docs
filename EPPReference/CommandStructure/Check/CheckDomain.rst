
.. index::
   pair: check; domain

Check domain
============

A domain check :ref:`command <struct-command>` is used to check
the availability of one or more domain names.

The domain check command is a ``check`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

The command must be contained in the ``<check>`` command class.

.. index:: Ⓔcheck, Ⓔname

Command element structure
-------------------------

The ``<domain:check>`` element must declare the ``domain`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<domain:name>`` **(1..n)**  – a domain name as :term:`eppcom:labelType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
      <check>
         <domain:check xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
            <domain:name>mydomain.cz</domain:name>
            <domain:name>somedomain.cz</domain:name>
         </domain:check>
      </check>
      <clTRID>dnix002#17-07-11at11:23:46</clTRID>
   </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > check_domain mydomain.cz somedomain.cz

.. index:: ⒺchkData, Ⓔcd, Ⓔname, Ⓔreason, ⓐavail, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<domain:chkData>`` which declares the ``domain`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<domain:cd>`` **(1..n)** – the check resolution of a single domain name:

   * ``<domain:name>`` **(1)** – the domain name as :term:`eppcom:labelType`,

      * ``@avail`` **(R)** – availability as :term:`xs:boolean`;
        ``true`` – available, ``false`` – not available,

   * ``<domain:reason>`` **(0..1)** – if the availability is negative,
     this element contains an explanation why the domain name is not available,
     as :term:`fredcom:msgType`.

      * ``@lang`` – language of the reason as :term:`xs:language`;
        default is ``en`` (English).

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
         <domain:chkData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.1.xsd">
            <domain:cd>
               <domain:name avail="1">mydomain.cz</domain:name>
            </domain:cd>
            <domain:cd>
               <domain:name avail="0">somedomain.cz</domain:name>
               <domain:reason>already registered.</domain:reason>
            </domain:cd>
         </domain:chkData>
      </resData>
      <trID>
         <clTRID>dnix002#17-07-11at11:23:46</clTRID>
         <svTRID>ReqID-0000139726</svTRID>
      </trID>
   </response>
   </epp>
