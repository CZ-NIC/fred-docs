
.. index::
   pair: check; nsset

Check nsset
=============

A nsset check :ref:`command <struct-command>` is used to check
the availability of one or more nsset handles.

The nsset check command is a ``check`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

The command must be contained in the ``<check>`` command class.

.. index:: Ⓔcheck, Ⓔid

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
         <check>
            <nsset:check xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.xsd">
               <nsset:id>NID-MYNSSET</nsset:id>
               <nsset:id>NID-NONE</nsset:id>
            </nsset:check>
         </check>
         <clTRID>hity005#17-07-12at11:18:08</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > check_nsset NID-MYNSSET NID-NONE

.. index:: ⒺchkData, Ⓔcd, Ⓔid, Ⓔreason, ⓐavail, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<nsset:chkData>`` which declares the ``nsset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<nsset:cd>`` **(1..n)** – the check resolution of a single nsset handle:

   * ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDType`,

      * ``@avail`` **(R)** – availability as :term:`xs:boolean`;
        ``true`` – available, ``false`` – not available,

   * ``<nsset:reason>`` **(0..1)** – if the availability is negative,
     this element contains an explanation why the nsset handle is not available,
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
            <nsset:chkData xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.1.xsd">
               <nsset:cd>
                  <nsset:id avail="0">NID-MYNSSET</nsset:id>
                  <nsset:reason>already registered.</nsset:reason>
               </nsset:cd>
               <nsset:cd>
                  <nsset:id avail="1">NID-NONE</nsset:id>
               </nsset:cd>
            </nsset:chkData>
         </resData>
         <trID>
            <clTRID>hity005#17-07-12at11:18:08</clTRID>
            <svTRID>ReqID-0000139774</svTRID>
         </trID>
      </response>
   </epp>
