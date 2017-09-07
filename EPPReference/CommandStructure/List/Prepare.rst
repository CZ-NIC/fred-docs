
.. index:: list

Prepare a list
==============

These commands are used to prepare lists of objects
which are managed by the authenticated client.
(In other words, of which the client is the :term:`designated registrar`.)

All list commands are elements in the ``fred`` namespace
(``http://www.nic.cz/xml/epp/fred-1.5``).

These commands are a part of the :doc:`protocol extension
</EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

.. index:: ⒺlistDomains, ⒺlistContacts, ⒺlistNssets, ⒺlistKeysets,
   ⒺdomainsByContact, ⒺdomainsByNsset, ⒺdomainsByKeyset,
   ⒺnssetsByContact, ⒺkeysetsByContact, ⒺnssetsByNs, Ⓔid, Ⓔname


Command element structure
-------------------------

The list command can be **one of** the following:

* ``<fred:listDomains/>`` **(1)** – select all domains as an empty element,
* ``<fred:listContacts/>`` **(1)** – select all contacts as an empty element,
* ``<fred:listNssets/>`` **(1)** – select all nssets as an empty element,
* ``<fred:listKeysets/>`` **(1)** – select all keysets as an empty element,
* ``<fred:domainsByContact>`` **(1)** – select domains by a contact (registrant or administrative contact),
   * ``<fred:id>`` **(1)** – a contact handle as :term:`fredcom:objIDType`,
* ``<fred:domainsByNsset>`` **(1)** – select domains by a nsset,
   * ``<fred:id>`` **(1)** – a nsset handle as :term:`fredcom:objIDType`,
* ``<fred:domainsByKeyset>`` **(1)** – select domains by a keyset,
   * ``<fred:id>`` **(1)** – a keyset handle as :term:`fredcom:objIDType`,
* ``<fred:nssetsByContact>`` **(1)** – select nssets by a technical contact,
   * ``<fred:id>`` **(1)** – a contact handle as :term:`fredcom:objIDType`,
* ``<fred:keysetsByContact>`` **(1)** – select keysets by a technical contact,
   * ``<fred:id>`` **(1)** – a contact handle as :term:`fredcom:objIDType`,
* ``<fred:nssetsByNs>`` **(1)** – select nssets by a name server,
   * ``<fred:name>`` **(1)** – a name-server hostname as :term:`eppcom:labelType`.

.. code-block:: xml
   :caption: Example of a parametrized listing command

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <extension>
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">
         <fred:domainsByContact>
            <fred:id>CID-ADMIN1</fred:id>
         </fred:domainsByContact>
         <fred:clTRID>ovcu002#17-08-11at12:26:39</fred:clTRID>
      </fred:extcommand>
   </extension>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > prep_domains_by_contact CID-ADMIN1

.. code-block:: xml
   :caption: Example of a simple listing command

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <extension>
         <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">
            <fred:listContacts/>
            <fred:clTRID>egrx002#17-08-30at18:49:12</fred:clTRID>
         </fred:extcommand>
      </extension>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > prep_contacts

.. index:: ⒺinfoResponse, Ⓔcount

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<fred:infoResponse>`` which declares the ``fred`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child element:

* ``<fred:count>`` **(1)** – the count of prepared items as :term:`xs:unsignedLong`.

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
         <fred:infoResponse xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.0.xsd">
            <fred:count>4</fred:count>
         </fred:infoResponse>
      </resData>
      <trID>
         <clTRID>ovcu002#17-08-11at12:26:39</clTRID>
         <svTRID>ReqID-0000141134</svTRID>
      </trID>
   </response>
   </epp>
