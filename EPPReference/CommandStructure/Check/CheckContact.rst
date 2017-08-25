
.. index::
   pair: check; contact

Check contact
=============

A contact check :ref:`command <struct-command>` is used to check
the availability of one or more contact handles.

The contact check command is a ``check`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

The command must be contained in the ``<check>`` command class.

.. index:: Ⓔcheck, Ⓔid

Command element structure
-------------------------

The ``<contact:check>`` element must declare the ``contact`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<contact:id>`` **(1..n)**  – a contact handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <check>
            <contact:check xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.xsd">
               <contact:id>CID-MYOWN</contact:id>
               <contact:id>CID-NONE</contact:id>
            </contact:check>
         </check>
         <clTRID>dyih007#17-07-11at15:35:42</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > check_contact CID-MYOWN CID-NONE

.. index:: ⒺchkData, Ⓔcd, Ⓔid, Ⓔreason, ⓐavail, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<contact:chkData>``  which declares the ``contact`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<contact:cd>`` **(1..n)** – the check resolution of a single contact handle:

   * ``<contact:id>`` **(1)** – the contact handle as :term:`fredcom:objIDType`,

      * ``@avail`` **(R)** – availability as :term:`xs:boolean`;
        ``true`` – available, ``false`` – not available,

   * ``<contact:reason>`` **(0..1)** – if the availability is negative,
     this element contains an explanation why the contact handle is not available,
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
            <contact:chkData xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.1.xsd">
               <contact:cd>
                  <contact:id avail="0">CID-MYOWN</contact:id>
                  <contact:reason>already registered.</contact:reason>
               </contact:cd>
               <contact:cd>
                  <contact:id avail="1">CID-NONE</contact:id>
               </contact:cd>
            </contact:chkData>
         </resData>
         <trID>
            <clTRID>dyih007#17-07-11at15:35:42</clTRID>
            <svTRID>ReqID-0000139763</svTRID>
         </trID>
      </response>
   </epp>
