
.. index:: update; keyset

Update keyset
=============

A keyset update command is used to alter the data of a keyset.

A keyset update command is an ``update`` element in the ``keyset`` namespace
(``http://www.nic.cz/xml/epp/keyset-1.3``).

.. index:: Ⓔupdate, Ⓔid,, Ⓔadd, Ⓔrem, Ⓔchg, Ⓔdnskey, Ⓔflags, Ⓔprotocol,
   Ⓔalg, ⒺpubKey, Ⓔtech, ⒺauthInfo

Command element structure
-------------------------

The ``<keyset:update>`` element must declare the ``keyset`` namespace
and schema and it must contain the following child elements:

* ``<keyset:id>`` **(1)**  – a keyset handle as :term:`fredcom:objIDType`,
* ``<keyset:add>`` **(0..1)** – a list of items that will be added to this keyset:

   * ``<keyset:dnskey>`` **(0..10)** – a DNS key (:ref:`see object's attributes
     for allowed values <mng-keyset-attr>`) given by:
      * ``<keyset:flags>`` **(1)** – flags as :term:`xs:unsignedShort`,
      * ``<keyset:protocol>`` **(1)** – protocol as :term:`xs:unsignedByte`,
      * ``<keyset:alg>`` **(1)** – algorithm as :term:`xs:unsignedByte`,
      * ``<keyset:pubKey>`` **(1)** – public key as :term:`keyset:keyT`,
   * ``<keyset:tech>`` **(0..n)** –  a handle of a contact that will be added
     to technical contacts as :term:`fredcom:objIDType`,

* ``<keyset:rem>`` **(0..1)** – a list of items that will be removed
  from this keyset:

   * ``<keyset:dnskey>`` **(0..10)** – a DNS key (:ref:`see object's attributes
     for allowed values <mng-keyset-attr>`) given by:
      * ``<keyset:flags>`` **(1)** – flags as :term:`xs:unsignedShort`,
      * ``<keyset:protocol>`` **(1)** – protocol as :term:`xs:unsignedByte`,
      * ``<keyset:alg>`` **(1)** – algorithm as :term:`xs:unsignedByte`,
      * ``<keyset:pubKey>`` **(1)** – public key as :term:`keyset:keyT`,
   * ``<keyset:tech>`` **(0..n)** – a handle of keyset's technical contact
     as :term:`fredcom:objIDType`,

* ``<keyset:chg>`` **(0..1)** – the new values of keyset attributes
  that will be replaced by this update. Omitted attributes will remain unchanged.

   * ``<keyset:authInfo>`` **(0..1)** – change the keyset's authorization
     information (transfer password) as :term:`fredcom:authInfoType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <update>
            <keyset:update xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
            xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.xsd">
               <keyset:id>KID-MYKEYSET</keyset:id>
               <keyset:add>
                  <keyset:dnskey>
                     <keyset:flags>257</keyset:flags>
                     <keyset:protocol>3</keyset:protocol>
                     <keyset:alg>5</keyset:alg>
                     <keyset:pubKey>eGVmbmZrY3lvcXFwamJ6aGt2YXhteXdkc2tjeXBp</keyset:pubKey>
                  </keyset:dnskey>
                  <keyset:dnskey>
                     <keyset:flags>257</keyset:flags>
                     <keyset:protocol>3</keyset:protocol>
                     <keyset:alg>5</keyset:alg>
                     <keyset:pubKey>aXN4Y2lpd2ZicWtkZHF4dnJyaHVtc3BreXN6ZGZy</keyset:pubKey>
                  </keyset:dnskey>
                  <keyset:tech>CID-TECH2</keyset:tech>
               </keyset:add>
               <keyset:rem>
                  <keyset:tech>CID-TECH1</keyset:tech>
               </keyset:rem>
               <keyset:chg>
                  <keyset:authInfo>aBcD234</keyset:authInfo>
               </keyset:chg>
            </keyset:update>
         </update>
         <clTRID>pkxv003#17-07-20at20:04:32</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > update_keyset KID-MYKEYSET (((257 3 5 eGVmbmZrY3lvcXFwamJ6aGt2YXhteXdkc2tjeXBp), (257 3 5 aXN4Y2lpd2ZicWtkZHF4dnJyaHVtc3BreXN6ZGZy)) () CID-TECH2) (() () CID-TECH1) aBcD234

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
