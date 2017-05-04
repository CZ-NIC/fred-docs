
.. index::
   pair: info; contact

Info contact
=============

A contact info command is an ``info`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

It is used to retrieve the data of a contact.

.. index:: Ⓔinfo, Ⓔid

Command element structure
-------------------------

The ``<contact:info>`` element must declare the ``contact`` namespace
and schema and it must contain the following child element:

* ``<contact:id>`` **(1)** the contact handle as :term:`fredcom:objIDType`.

.. rubric:: Example

.. code-block:: xml

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

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > info_contact CID-MYCONTACT


.. index:: ⒺinfData, Ⓔroid, Ⓔstatus,
   Ⓔid, ⒺpostalInfo, Ⓔname, Ⓔorg, Ⓔaddr, Ⓔstreet,
   Ⓔcity, Ⓔsp, Ⓔpc, Ⓔcc, Ⓔvoice, Ⓔfax, Ⓔemail, ⒺauthInfo,
   ⒺclID, ⒺcrID, ⒺcrDate, ⒺupID, ⒺupDate, ⒺtrDate,
   Ⓔdisclose, Ⓔvat, Ⓔident, ⒺnotifyEmail, ⓐtype, ⓐflag,
   ⓐs, ⓐlang

Response element structure
--------------------------

The response message contains the ``result`` and ``resData`` with information
about the requested contact contained in an ``infData`` element
in the ``contact`` namespace (``contact-full-ns``).

The ``<contact:infData>`` element declares the namespace and schema
and contains the following child elements:

* ``<contact:id>`` **(1)** the contact handle as :term:`fredcom:objIDType`,
* ``<contact:roid>`` **(1)** the contact repository identifier as :term:`eppcom:roidType`,
* ``<contact:status>`` **(0..10)** the contact object state(s):
   * ``@s`` **(R)** attribute (state value) as one of values:
      * ``ok``
      * ``linked``
      * ``serverTransferProhibited``
      * ``serverDeleteProhibited``
      * ``serverUpdateProhibited``
      * ``deleteCandidate``
      * ``conditionallyIdentifiedContact``
      * ``identifiedContact``
      * ``validatedContact``
      * ``mojeidContact``
   * ``@lang`` attribute (language of the state description) as a :term:`xs:language` (default: ``en``),
   * element content: the state description as a :term:`xs:normalizedString`,
* ``<contact:postalInfo>`` **(1)** – contact's postal information:
   * ``<contact:name>`` **(0..1)** – personal name as :term:`contact:postalLineType`,
   * ``<contact:org>`` **(0..1)** – organization name as :term:`contact:optPostalLineType`,
   * ``<contact:addr>`` **(0..1)** – address:
      * ``<contact:street>`` **(0..3)** – street line 1–3 as :term:`contact:optPostalLineType`,
      * ``<contact:city>`` **(0..1)** – city as :term:`contact:postalLineType`,
      * ``<contact:sp>`` **(0..1)** – state or province as :term:`contact:optPostalLineType`,
      * ``<contact:pc>`` **(0..1)** – postal code as :term:`contact:pcType`,
      * ``<contact:cc>`` **(0..1)** – country code as :term:`contact:ccType`,
* ``<contact:voice>`` **(0..1)** – phone number as :term:`contact:e164StringType`,
* ``<contact:fax>`` **(0..1)** – fax number as :term:`contact:e164StringType`,
* ``<contact:email>`` **(0..1)** – email as :term:`contact:emailCommaListType`,
* ``<contact:authInfo>`` **(0..1)** – authorization information (transfer password) as :term:`fredcom:authInfoType`,
* ``<contact:clID>`` **(1)** – designated registrar handle as :term:`eppcom:clIDType`,
* ``<contact:crID>`` **(1)** – handle of the registrar who created this contact as :term:`eppcom:clIDType`,
* ``<contact:crDate>`` **(1)** – date of creation as :term:`xs:dateTime`,
* ``<contact:upID>`` **(0..1)** – handle of the registrar who was the last to update this contact as :term:`eppcom:clIDType`,
* ``<contact:upDate>`` **(0..1)** – date of the last update as :term:`xs:dateTime`,
* ``<contact:trDate>`` **(1)** – date of the last transfer (?) as :term:`xs:dateTime`,
* ``<contact:disclose>`` **(0..1)** – contact information disclosure settings:
   * ``@flag`` **(R)** attribute (disclose flag) as a :term:`xs:boolean`: ``0`` – listed items are hidden, ``1`` – listed items are published,
   * ``<contact:addr/>`` **(0..1)** – address disclosure setting as an empty element,
   * ``<contact:voice/>`` **(0..1)** – voice disclosure setting as an empty element,
   * ``<contact:fax/>`` **(0..1)** – fax disclosure setting as an empty element,
   * ``<contact:email/>`` **(0..1)** – email disclosure setting as an empty element,
   * ``<contact:vat/>`` **(0..1)** – VAT number disclosure setting as an empty element,
   * ``<contact:ident/>`` **(0..1)** – identity document disclosure setting as an empty element,
   * ``<contact:notifyEmail/>`` **(0..1)** – notification email disclosure setting as an empty element,

   .. Note:: ???, depends on the disclosure policy of the server.

* ``<contact:vat>`` **(0..1)** – :term:`VAT`-payer identifier as a :term:`contact:vatT`,
* ``<contact:ident>`` **(0..1)** – identity-document identification:
   * ``@type`` **(R)** attribute (the type of the identity document)
     as one of values: ``op`` (identity card number),
     ``passport`` (passport number),
     ``mpsv`` (number from the Ministry of Labour and Social Affairs),
     ``ico`` (company number), ``birthday`` (birthday date),
   * element content: an identification number as a :term:`contact:identValueT`,
* ``<contact:notifyEmail>`` **(0..1)** – notification email as :term:`contact:emailCommaListType`.


.. rubric:: Example

.. code-block:: xml

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
