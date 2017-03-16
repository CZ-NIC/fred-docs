
.. index::
   pair: create; contact

Create contact
==============

.. todo:: TODO

Contact creation is a ``create`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

.. index:: Ⓔcreate, Ⓔid, Ⓔchg, ⒺpostalInfo, Ⓔname, Ⓔorg, Ⓔaddr, Ⓔstreet,
   Ⓔcity, Ⓔsp, Ⓔpc, Ⓔcc, Ⓔvoice, Ⓔfax, Ⓔemail, ⒺauthInfo,
   Ⓔdisclose, Ⓔvat, Ⓔident, ⒺnotifyEmail, ⓐtype, ⓐflag

Command element structure
-------------------------

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
   <create>
      <contact:create xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.xsd">
      <contact:id>CID-BEBA</contact:id>
      <contact:postalInfo>
         <contact:name>Bea Bayer</contact:name>
         <contact:addr>
            <contact:street>Masarykova 12</contact:street>
            <contact:city>Brno</contact:city>
            <contact:pc>60200</contact:pc>
            <contact:cc>CZ</contact:cc>
         </contact:addr>
      </contact:postalInfo>
      <contact:voice>+420.555666777</contact:voice>
      <contact:fax>+420.555666888</contact:fax>
      <contact:email>bea@bayer.cz</contact:email>
      <contact:authInfo>myauthpwd</contact:authInfo>
      <contact:disclose flag="0">
         <contact:vat/>
         <contact:ident/>
      </contact:disclose>
      <contact:vat>cz8054121234</contact:vat>
      <contact:ident type="op">12345678910</contact:ident>
      <contact:notifyEmail>notify.bea@bayer.cz</contact:notifyEmail>
      </contact:create>
   </create>
   <clTRID>vyfn011#17-03-31at13:31:02</clTRID>
   </command>
   </epp>



.. rubric:: FRED-client equivalent

.. code-block:: shell

   > create_contact CID-BEBA 'Bea Bayer' bea@bayer.cz 'Masarykova 12' Brno 60200 CZ NULL NULL myauthpwd +420.555666777 +420.555666888 (y (voice,fax,email,notify_email)) cz8054121234 (12345678910 op) notify.bea@bayer.cz



Response element structure
--------------------------

.. rubric:: Example

.. code-block:: xml

   <epp/>
