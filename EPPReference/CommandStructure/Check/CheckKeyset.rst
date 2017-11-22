
.. index::
   pair: check; keyset

Check keyset
=============

A keyset check :ref:`command <struct-command>` is used to check
the availability of one or more keyset handles.

The keyset check command is a ``check`` element in the ``keyset`` namespace
(``http://www.nic.cz/xml/epp/keyset-1.3``).

The command must be contained in the ``<check>`` command type.

.. index:: Ⓔcheck, Ⓔid

Command element structure
-------------------------

The ``<keyset:check>`` element must declare the ``keyset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<keyset:id>`` **(1..n)**  – a keyset handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <check>
            <keyset:check xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.2.xsd">
               <keyset:id>KID-MYKEYSET</keyset:id>
               <keyset:id>KID-NONE</keyset:id>
            </keyset:check>
         </check>
         <clTRID>ygxv005#17-07-12at13:06:45</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > check_keyset KID-MYKEYSET KID-NONE

.. index:: ⒺchkData, Ⓔcd, Ⓔid, Ⓔreason, ⓐavail, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data, and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<keyset:chkData>`` which declares the ``keyset`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<keyset:cd>`` **(1..n)** – the check resolution of a single keyset handle:

   * ``<keyset:id>`` **(1)** – the keyset handle as :term:`fredcom:objIDType`,

      * ``@avail`` **(R)** – availability as :term:`xs:boolean`;
        ``true`` – available, ``false`` – not available,

   * ``<keyset:reason>`` **(0..1)** – if the availability is negative,
     this element contains an explanation why the keyset handle is not available,
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
            <keyset:chkData xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.2.xsd">
               <keyset:cd>
                  <keyset:id avail="0">KID-MYKEYSET</keyset:id>
                  <keyset:reason>already registered.</keyset:reason>
               </keyset:cd>
               <keyset:cd>
                  <keyset:id avail="1">KID-NONE</keyset:id>
               </keyset:cd>
            </keyset:chkData>
         </resData>
         <trID>
            <clTRID>ygxv005#17-07-12at13:06:45</clTRID>
            <svTRID>ReqID-0000139780</svTRID>
         </trID>
      </response>
   </epp>
