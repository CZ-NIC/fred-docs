
.. index::
   pair: update; contact

Update contact
==============

Contact update is an ``update`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

.. index:: Ⓔupdate, Ⓔid, Ⓔchg, ⒺpostalInfo, Ⓔname, Ⓔorg, Ⓔaddr, Ⓔstreet,
   Ⓔcity, Ⓔsp, Ⓔpc, Ⓔcc, Ⓔvoice, Ⓔfax, Ⓔemail, ⒺauthInfo,
   Ⓔdisclose, Ⓔvat, Ⓔident, ⒺnotifyEmail, ⓐtype, ⓐflag

Command element structure
-------------------------

The ``<contact:update>`` element must declare the ``contact`` namespace
and schema and it must contain the following child elements:

* ``<contact:id>`` **(1)** the contact handle as :term:`fred:objIDType`.
* ``<contact:chg>`` **(0..1)** comprises the new values of contact data
  that will be changed by this update. Omitted properties will remain unchanged.

   * ``<contact:postalInfo>`` **(0..1)** – change contact's postal information:
      * ``<contact:name>`` **(0..1)** – personal name as :term:`contact:postalLineType`,
      * ``<contact:org>`` **(0..1)** – organization name as :term:`contact:optPostalLineType`,
      * ``<contact:addr>`` **(0..1)** – address:
         * ``<contact:street>`` **(1..3)** – street line 1–3 as :term:`contact:optPostalLineType`,
         * ``<contact:city>`` **(1)** – city as :term:`contact:postalLineType`,
         * ``<contact:sp>`` **(0..1)** – state or province as :term:`contact:optPostalLineType`,
         * ``<contact:pc>`` **(1)** – postal code as :term:`xs:token` of the maximum length of 16 characters,
         * ``<contact:cc>`` **(1)** – country code as :term:`xs:token` of the length of 2 characters,
   * ``<contact:voice>`` **(0..1)** – change phone number as :term:`contact:e164StringType`,
   * ``<contact:fax>`` **(0..1)** – change fax number as :term:`contact:e164StringType`,
   * ``<contact:email>`` **(0..1)** – change email as :term:`contact:emailCommaListType`,
   * ``<contact:authInfo>`` **(0..1)** – change authorization information as :term:`fred:authInfoType`
   * ``<contact:disclose>`` **(0..1)** – change contact information disclosure settings:
      * ``@flag`` **(R)** attribute (disclose flag) as a :term:`xs:boolean`: ``0`` – hide listed items, ``1`` – publish listed items,
      * ``<contact:addr/>`` **(0..1)** – address disclosure setting as an empty element,
      * ``<contact:voice/>`` **(0..1)** – voice disclosure setting as an empty element,
      * ``<contact:fax/>`` **(0..1)** – fax disclosure setting as an empty element,
      * ``<contact:email/>`` **(0..1)** – email disclosure setting as an empty element,
      * ``<contact:vat/>`` **(0..1)** – VAT number disclosure setting as an empty element,
      * ``<contact:ident/>`` **(0..1)** – identity document disclosure setting as an empty element,
      * ``<contact:notifyEmail/>`` **(0..1)** – notification email disclosure setting as an empty element.

      .. Note:: Whether the new disclosure settings will have an effect, depends on the disclosure policy of the server.

   * ``<contact:vat>`` **(0..1)** – change :term:`VAT`-payer identifier as a :term:`contact:vatT`,
   * ``<contact:ident>`` **(0..1)** – change identity-document identification:
      * ``@type`` **(R)** attribute (the type of the identity document)
        as one of values: ``op`` (identity card number),
        ``passport`` (passport number),
        ``mpsv`` (number from the Ministry of Labour and Social Affairs),
        ``ico`` (company number), ``birthday`` (birthday date),
      * an identification number as a :term:`contact:identValueT`,
   * ``<contact:notifyEmail>`` **(0..1)** – change notification email as :term:`contact:emailUpdCommaListType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
   <update>
      <contact:update
       xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.xsd">
      <contact:id>CID-BEBA</contact:id>
      <contact:chg>
         <contact:notifyEmail>change.only@notify-email.cz</contact:notifyEmail>
      </contact:chg>
      </contact:update>
   </update>
   <clTRID>mhvo002#17-03-31at15:00:34</clTRID>
   </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > update_contact CID-BEBA (() NULL NULL NULL NULL () NULL () change.only@notify-email.cz)

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result <plain-result>` message
which does not contain any return values (no ``resData``).
