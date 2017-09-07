
.. index::
   pair: info; contact

Info contact
=============

A contact info :ref:`command <struct-command>` is used to view details of a contact.

The contact info command is an ``info`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

The command must be contained in the ``<info>`` command type.

.. index:: Ⓔinfo, Ⓔid

Command element structure
-------------------------

The ``<contact:info>`` element must declare the ``contact`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<contact:id>`` **(1)** – the contact handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
   <info>
      <contact:info xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.xsd">
         <contact:id>CID-MYCONTACT</contact:id>
      </contact:info>
   </info>
   <clTRID>zmge004#17-05-04at12:20:55</clTRID>
   </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > info_contact CID-MYCONTACT


.. index:: ⒺinfData, Ⓔroid, Ⓔstatus,
   Ⓔid, ⒺpostalInfo, Ⓔname, Ⓔorg, Ⓔaddr, Ⓔstreet,
   Ⓔcity, Ⓔsp, Ⓔpc, Ⓔcc, Ⓔvoice, Ⓔfax, Ⓔemail, ⒺauthInfo,
   ⒺclID, ⒺcrID, ⒺcrDate, ⒺupID, ⒺupDate, ⒺtrDate,
   Ⓔdisclose, Ⓔvat, Ⓔident, ⒺnotifyEmail, ⓐtype, ⓐflag,
   ⓐs, ⓐlang

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

.. _contact-infdata:

The response data element (``<resData>``) contains a single child element
``<contact:infData>``  which declares the ``contact`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<contact:id>`` **(1)** – the contact handle as :term:`fredcom:objIDType`,
* ``<contact:roid>`` **(1)** – the contact repository identifier as :term:`eppcom:roidType`,
* ``<contact:status>`` **(1..n)** – the :ref:`contact object state(s) <mng-contact-stat>`:
   * ``@s`` **(R)** – state name as one of values:
      * ``ok``
      * ``linked``
      * ``serverTransferProhibited``
      * ``serverDeleteProhibited``
      * ``serverUpdateProhibited``
      * ``serverBlocked``
      * ``deleteCandidate``
      * ``conditionallyIdentifiedContact``
      * ``identifiedContact``
      * ``validatedContact``
      * ``mojeidContact``
   * ``@lang`` – language of the state description as a :term:`xs:language` (default: ``en``),
   * element content: the state description as a :term:`xs:normalizedString`,
* ``<contact:postalInfo>`` **(1)** – contact's postal information:
   * ``<contact:name>`` **(0..1)** – the person name as :term:`contact:postalLineType`,
   * ``<contact:org>`` **(0..1)** – the organization name as :term:`contact:optPostalLineType`,
   * ``<contact:addr>`` **(0..1)** – the postal address:
      * ``<contact:street>`` **(0..3)** – the street line(s) as :term:`contact:optPostalLineType`,
      * ``<contact:city>`` **(0..1)** – the city as :term:`contact:postalLineType`,
      * ``<contact:sp>`` **(0..1)** – the state or province as :term:`contact:optPostalLineType`,
      * ``<contact:pc>`` **(0..1)** – the postal code as :term:`contact:pcType`,
      * ``<contact:cc>`` **(0..1)** – the country code as :term:`contact:ccType`,
* ``<contact:voice>`` **(0..1)** – the phone number as :term:`contact:e164StringType`,
* ``<contact:fax>`` **(0..1)** – the fax number as :term:`contact:e164StringType`,
* ``<contact:email>`` **(0..1)** – a comma-separated list of email addresses as :term:`contact:emailCommaListType`,
* ``<contact:authInfo>`` **(0..1)** – authorization information (transfer password) as :term:`fredcom:authInfoType`,
* ``<contact:clID>`` **(1)** – the designated registrar's handle as :term:`eppcom:clIDType`,
* ``<contact:crID>`` **(1)** – the handle of the registrar who created this contact as :term:`eppcom:clIDType`,
* ``<contact:crDate>`` **(1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`,
* ``<contact:upID>`` **(0..1)** – the handle of the registrar who was the last to update this contact as :term:`eppcom:clIDType`,
* ``<contact:upDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last update as :term:`xs:dateTime`,
* ``<contact:trDate>`` **(0..1)** – the :ref:`timestamp <mngobj-timestamps>` of the last transfer as :term:`xs:dateTime`,
* ``<contact:disclose>`` **(0..1)** – contact information disclosure settings:
   * ``@flag`` **(R)** – disclose flag as a :term:`xs:boolean`: ``0`` – listed items are hidden, ``1`` – listed items are published,
   * ``<contact:addr/>`` **(0..1)** – the address disclosure setting as an empty element,
   * ``<contact:voice/>`` **(0..1)** – the voice disclosure setting as an empty element,
   * ``<contact:fax/>`` **(0..1)** – the fax disclosure setting as an empty element,
   * ``<contact:email/>`` **(0..1)** – the email disclosure setting as an empty element,
   * ``<contact:vat/>`` **(0..1)** – the VAT number disclosure setting as an empty element,
   * ``<contact:ident/>`` **(0..1)** – the identity document disclosure setting as an empty element,
   * ``<contact:notifyEmail/>`` **(0..1)** – the notification email disclosure setting as an empty element,
* ``<contact:vat>`` **(0..1)** – the :term:`VAT`-payer identifier as a :term:`contact:vatT`,
* ``<contact:ident>`` **(0..1)** – identity-document identification:
   * ``@type`` **(R)** – the type of the identity document as one of values:
     ``op`` (identity card number), ``passport`` (passport number),
     ``mpsv`` (number from the Ministry of Labour and Social Affairs),
     ``ico`` (company number), ``birthday`` (the date of birth),
   * element content: the identification number as a :term:`contact:identValueT`,
* ``<contact:notifyEmail>`` **(0..1)** – a comma-separated list of email addresses for notification as :term:`contact:emailCommaListType`.

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
      <contact:infData xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.1.xsd">
         <contact:id>CID-MYCONTACT</contact:id>
         <contact:roid>C0009746170-CZ</contact:roid>
         <contact:status s="linked">Has relation to other records in the registry</contact:status>
         <contact:postalInfo>
            <contact:name>Name Surname</contact:name>
            <contact:addr>
               <contact:street>Street</contact:street>
               <contact:city>City</contact:city>
               <contact:pc>12345</contact:pc>
               <contact:cc>CZ</contact:cc>
            </contact:addr>
         </contact:postalInfo>
         <contact:email>email@example.com</contact:email>
         <contact:clID>REG-MYREG</contact:clID>
         <contact:crID>REG-MYREG</contact:crID>
         <contact:crDate>2017-05-04T11:30:25+02:00</contact:crDate>
         <contact:authInfo>PfLyxPC4</contact:authInfo>
         <contact:disclose flag="0"/>
      </contact:infData>
      </resData>
      <trID>
         <clTRID>zmge004#17-05-04at12:20:55</clTRID>
         <svTRID>ReqID-0000132810</svTRID>
      </trID>
   </response>
   </epp>
