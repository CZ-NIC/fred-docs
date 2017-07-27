
.. index:: update; domain

Update domain
=============

A domain update command is used to alter the data of a domain.

A domain update command is an ``update`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

.. index:: Ⓔupdate, Ⓔname, Ⓔadd, Ⓔrem, Ⓔchg, Ⓔadmin, Ⓔtempcontact, Ⓔnsset,
   Ⓔkeyset, Ⓔregistrant, ⒺauthInfo

Command element structure
-------------------------

The ``<domain:update>`` element must declare the ``domain`` namespace
and schema and it must contain the following child elements:

* ``<domain:name>`` **(1)** – the domain name as :term:`eppcom:labelType`,
* ``<domain:add>`` **(0..1)** – a list of contact handles that will
  be added to the list of administration contacts of this domain:

   * ``<domain:admin>`` **(0..n)** – a contact handle as :term:`fredcom:objIDType`,
* ``<domain:rem>`` **(0..1)** – a list of contact handles that will
  be removed from the list of administration contacts of this domain:

   * ``<domain:admin>`` **(0..n)** – a contact handle as :term:`fredcom:objIDType`,
* ``<domain:chg>`` **(0..1)** – the new values of domain attributes
  that will be changed by this update. Omitted attributes will remain unchanged.

   * ``<domain:nsset>`` **(0..1)** – change the domain's nsset by its handle
     as :term:`fredcom:objIDChgType`,
   * ``<domain:keyset>`` **(0..1)** – change the domain's keyset by its handle
     as :term:`fredcom:objIDChgType`,
   * ``<domain:registrant>`` **(0..1)** – change the domain's registrant by its
     handle as :term:`fredcom:objIDType`,
   * ``<domain:authInfo>`` **(0..1)** – change the domain's authorization
     information (transfer password) as :term:`fredcom:authInfoType`.


.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <update>
            <domain:update xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
               <domain:name>mydomain.cz</domain:name>
               <domain:add>
                  <domain:admin>CID-ADMIN2</domain:admin>
               </domain:add>
               <domain:rem>
                  <domain:admin>CID-ADMIN1</domain:admin>
               </domain:rem>
               <domain:chg>
                  <domain:nsset>NID-MYNSSET</domain:nsset>
                  <domain:registrant>CID-MYOWN</domain:registrant>
               </domain:chg>
            </domain:update>
         </update>
         <clTRID>uafh003#17-07-18at10:45:41</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > update_domain mydomain.cz CID-ADMIN2 CID-ADMIN1 () (NID-MYNSSET NULL CID-MYOWN)

.. index:: ⒺvalExDate, Ⓔpublish

ENUM extension
^^^^^^^^^^^^^^

The ``<domain:update>`` element is used in the same way as described above.

The :ref:`command extension <command-ext>` can be used to change the validation
of an ENUM domain and/or its publish flag.

The command's ``<extension>`` element must contain a **single** ``<enumval:update>``
element which declares the ``enumval`` namespace (``http://www.nic.cz/xml/epp/enumval-1.2``)
and schema and contains:

* ``<enumval:valExDate>`` **(0..1)**  – a new validation expiration date as :term:`xs:date`;
  the new date must be within range – see :ref:`the explanation in RenewDomain <new-valexdate>`,

* ``<enumval:publish>`` **(0..1)** – a new setting for publishing the ENUM
  domain in a public directory as :term:`xs:boolean`; ``true`` – display, ``false`` – hide.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <update>
            <domain:update xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
               <domain:name>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</domain:name>
            </domain:update>
         </update>
         <extension>
            <enumval:update xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.xsd">
               <enumval:chg>
                  <enumval:valExDate>2018-01-02</enumval:valExDate>
               </enumval:chg>
            </enumval:update>
         </extension>
         <clTRID>cant003#17-07-18at10:49:42</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > update_domain 1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa () () () () 2018-01-02

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.

ENUM extension
^^^^^^^^^^^^^^

:ref:`Response extension <response-ext>` is not used in reply to this command.
