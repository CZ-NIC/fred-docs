
.. index::
   pair: update; contact

Update contact
==============

A contact update :ref:`command <struct-command>` is used to alter details of a contact.

The contact update command is an ``update`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

The command must be contained in the ``<update>`` command type.

.. index:: Ⓔupdate, Ⓔid, Ⓔchg, ⒺpostalInfo, Ⓔname, Ⓔorg, Ⓔaddr, Ⓔstreet,
   Ⓔcity, Ⓔsp, Ⓔpc, Ⓔcc, Ⓔvoice, Ⓔfax, Ⓔemail, ⒺauthInfo,
   Ⓔdisclose, Ⓔvat, Ⓔident, ⒺnotifyEmail, ⓐtype, ⓐflag

Command element structure
-------------------------

The ``<contact:update>`` element must declare the ``contact`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<contact:id>`` **(1)** – the contact handle as :term:`fredcom:objIDType`.
* ``<contact:chg>`` **(0..1)** – comprises the new values of contact attributes
  that will be changed by this update. Omitted attributes will remain unchanged.

   * ``<contact:postalInfo>`` **(0..1)** – change contact's postal information:
      * ``<contact:name>`` **(0..1)** – personal name as :term:`contact:postalLineType`,
      * ``<contact:org>`` **(0..1)** – organization name as :term:`contact:optPostalLineType`,
      * ``<contact:addr>`` **(0..1)** – address:
         * ``<contact:street>`` **(1..3)** – street line 1–3 as :term:`contact:optPostalLineType`,
         * ``<contact:city>`` **(1)** – city as :term:`contact:postalLineType`,
         * ``<contact:sp>`` **(0..1)** – state or province as :term:`contact:optPostalLineType`,
         * ``<contact:pc>`` **(1)** – postal code as :term:`contact:pcType`,
         * ``<contact:cc>`` **(1)** – country code as :term:`contact:ccType`,
   * ``<contact:voice>`` **(0..1)** – change phone number as :term:`contact:e164StringType`,
   * ``<contact:fax>`` **(0..1)** – change fax number as :term:`contact:e164StringType`,
   * ``<contact:email>`` **(0..1)** – change email as :term:`contact:emailCommaListType`,
   * ``<contact:authInfo>`` **(0..1)** – change authorization information (transfer password) as :term:`fredcom:authInfoType`
   * ``<contact:disclose>`` **(0..1)** – change contact information disclosure settings:
      * ``@flag`` **(R)** – disclose flag as a :term:`xs:boolean`: ``0`` – hide listed items, ``1`` – publish listed items,
      * ``<contact:addr/>`` **(0..1)** – address disclosure setting as an empty element,
      * ``<contact:voice/>`` **(0..1)** – voice disclosure setting as an empty element,
      * ``<contact:fax/>`` **(0..1)** – fax disclosure setting as an empty element,
      * ``<contact:email/>`` **(0..1)** – email disclosure setting as an empty element,
      * ``<contact:vat/>`` **(0..1)** – VAT number disclosure setting as an empty element,
      * ``<contact:ident/>`` **(0..1)** – identity document disclosure setting as an empty element,
      * ``<contact:notifyEmail/>`` **(0..1)** – notification email disclosure setting as an empty element.

      .. Note:: Omitted items will be reset by the server according to its data-collection policy.

         Whether the new disclosure settings will have an effect, also depends on the server's policy.

   * ``<contact:vat>`` **(0..1)** – change :term:`VAT`-payer identifier as a :term:`contact:vatT`,
   * ``<contact:ident>`` **(0..1)** – change identity-document identification:
      * ``@type`` **(R)** – the type of the identity document
        as one of values: ``op`` (identity card number),
        ``passport`` (passport number),
        ``mpsv`` (number from the Ministry of Labour and Social Affairs),
        ``ico`` (company number), ``birthday`` (the date of birth),
      * element content: an identification number as a :term:`contact:identValueT`,
   * ``<contact:notifyEmail>`` **(0..1)** – change notification email as :term:`contact:emailUpdCommaListType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <update>
            <contact:update xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
               <contact:id>CID-MYOWN</contact:id>
               <contact:chg>
                  <contact:voice>+420.222333444</contact:voice>
                  <contact:disclose flag="0">
                     <contact:voice/>
                  </contact:disclose>
               </contact:chg>
            </contact:update>
         </update>
         <clTRID>rxzw005#17-07-18at12:03:30</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > update_contact CID-MYOWN (() +420.222333444 NULL NULL NULL (n voice))

.. index:: Ⓔmailing, Ⓔaddr

Mailing address extension
^^^^^^^^^^^^^^^^^^^^^^^^^

The ``<contact:update>`` element is used in the same way as described above.

The :ref:`command extension <command-ext>` can be used to set or remove the mailing address.

The command's ``<extension>`` element must contain a **single** ``<extra-addr:update>``
element which declares the ``extra-addr`` namespace (``http://www.nic.cz/xml/epp/extra-addr-1.0``)
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and contains:

* ``<extra-addr:set>`` **(0..1)** – a new address will be set;
  if the contact already has a mailing address, it will be replaced:

   * ``<extra-addr:mailing>`` **(1)**  – mailing address container:
      * ``<extra-addr:addr>`` **(1)** – address:
         * ``<extra-addr:street>`` **(1..3)** – street line 1–3 as :term:`extra-addr:postalLineType`,
         * ``<extra-addr:city>`` **(1)** – city as :term:`extra-addr:postalLineType`,
         * ``<extra-addr:sp>`` **(0..1)** – state or province as :term:`extra-addr:postalLineType`,
         * ``<extra-addr:pc>`` **(1)** – postal code as :term:`extra-addr:pcType`,
         * ``<extra-addr:cc>`` **(1)** – country code as :term:`extra-addr:ccType`,

* ``<extra-addr:rem>`` **(0..1)** – an address will be removed from the contact:
   * ``<extra-addr:mailing/>`` **(1)**  – the mailing address must be specified as an empty element.


.. code-block:: xml
   :caption: Example (set)

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <update>
            <contact:update
             xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
               <contact:id>CID-EXTRAADDR</contact:id>
               <contact:chg>
                  <contact:voice>+420.000000001</contact:voice>
                  <contact:notifyEmail>foobar-notify@nic.cz</contact:notifyEmail>
               </contact:chg>
            </contact:update>
         </update>
         <extension>
            <extra-addr:update
             xmlns:extra-addr="http://www.nic.cz/xml/epp/extra-addr-1.0"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/extra-addr-1.0 extra-addr-1.0.0.xsd">
               <extra-addr:set>
                  <extra-addr:mailing>
                     <extra-addr:addr>
                        <extra-addr:street>Kratka 24</extra-addr:street>
                        <extra-addr:city>Praha</extra-addr:city>
                        <extra-addr:pc>11150</extra-addr:pc>
                        <extra-addr:cc>CZ</extra-addr:cc>
                     </extra-addr:addr>
                  </extra-addr:mailing>
               </extra-addr:set>
            </extra-addr:update>
         </extension>
         <clTRID>zbab002#15-08-25at17:37:28</clTRID>
      </command>
   </epp>

.. code-block:: xml
   :caption: Example (remove)

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <update>
            <contact:update xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
               <contact:id>CID-EXTRAADDR</contact:id>
               <contact:chg>
                  <contact:voice>+420.000000001</contact:voice>
                  <contact:notifyEmail>foobar-notify@nic.cz</contact:notifyEmail>
               </contact:chg>
            </contact:update>
         </update>
         <extension>
            <extra-addr:update
             xmlns:extra-addr="http://www.nic.cz/xml/epp/extra-addr-1.0"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/extra-addr-1.0 extra-addr-1.0.0.xsd">
               <extra-addr:rem>
                  <extra-addr:mailing/>
               </extra-addr:rem>
            </extra-addr:update>
         </extension>
         <clTRID>zbab002#15-08-25at17:37:28</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > # This command does not have a FRED-client equivalent in this version.

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
