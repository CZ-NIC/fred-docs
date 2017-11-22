
.. index::
   pair: domain; create

Create domain
=============

A domain create :ref:`command <struct-command>` is used to register a new domain.

The contact create command is a ``create`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

The command must be contained in the ``<create>`` command type.

.. index:: Ⓔcreate, Ⓔname, Ⓔperiod, Ⓔnsset, Ⓔkeyset, Ⓔregistrant, Ⓔadmin,
   ⒺauthInfo, ⓐunit

Command element structure
-------------------------

The ``<domain:create>`` element must declare the ``domain`` :doc:`namespace and
schema </EPPReference/SchemasNamespaces/index>`, and it must contain the following child elements:

* ``<domain:name>`` **(1)**  – a domain name as :term:`eppcom:labelType`,
* ``<domain:period>`` **(0..1)**  – the registration period
  as :term:`domain:pLimitType`,

   * ``@unit`` **(R)**  – the unit the period is counted in; it can be
     either ``m`` for months or ``y`` for years.

  If omitted, the domain expiration is set to the minimum. (FRED's default: 1 year)

* ``<domain:nsset>`` **(0..1)** – a nsset handle to associate as :term:`fredcom:objIDType`,
* ``<domain:keyset>`` **(0..1)** – the keyset handle to associate as :term:`fredcom:objIDType`,
* ``<domain:registrant>`` **(1)** – the domain owner handle as :term:`fredcom:objIDType`,
* ``<domain:admin>`` **(0..n)** – an administrative contact handle as :term:`fredcom:objIDType`,
* ``<domain:authInfo>`` **(0..1)** – authorization information (transfer password)
  as :term:`fredcom:authInfoType`; if omitted, the password will be generated
  by the server.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <create>
            <domain:create xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>thisdomain.cz</domain:name>
               <domain:nsset>NID-MYNSSET</domain:nsset>
               <domain:registrant>CID-MYOWN</domain:registrant>
               <domain:admin>CID-ADMIN1</domain:admin>
            </domain:create>
         </create>
         <clTRID>zbdm002#17-08-09at12:31:47</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > create_domain thisdomain.cz CID-MYOWN NULL NID-MYNSSET NULL () CID-ADMIN1

.. index:: ⒺvalExDate, Ⓔpublish

ENUM extension
^^^^^^^^^^^^^^

The ``<domain:create>`` element is used in the same way as described above.

The :ref:`command extension <command-ext>` can be used to set the validation
and/or the publish flag of an ENUM domain at the time of creation.
Otherwise you can set the validation and/or publish flag later
with the :doc:`domain:update <../Update/UpdateDomain>`, or you can change the
validation when renewing the domain with the :doc:`domain:renew <../RenewDomain>`
command.

The command's ``<extension>`` element must contain a **single** ``<enumval:create>``
element which declares the ``enumval`` namespace (``http://www.nic.cz/xml/epp/enumval-1.2``)
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and contains:

* ``<enumval:valExDate>`` **(0..1)**  – a validation expiration date as :term:`xs:date`;
  the date must range from ``tomorrow`` to ``today + max. validation period``,

* ``<enumval:publish>`` **(0..1)** – a setting for publishing the ENUM
  domain in a public directory as :term:`xs:boolean`; ``true`` – display,
  ``false`` – hide (default).

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <create>
            <domain:create xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>2.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</domain:name>
               <domain:period unit="y">1</domain:period>
               <domain:registrant>CID-MYOWN</domain:registrant>
            </domain:create>
         </create>
         <extension>
            <enumval:create xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.0.xsd">
               <enumval:valExDate>2018-02-09</enumval:valExDate>
            </enumval:create>
         </extension>
         <clTRID>zbdm003#17-08-09at12:39:34</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > create_domain 2.1.1.7.4.5.2.2.2.0.2.4.e164.arpa CID-MYOWN NULL NULL NULL (1 y) () 2018-02-09

.. index:: ⒺcreData, Ⓔname, ⒺcrDate, ⒺexDate

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data, and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<domain:creData>``  which declares the ``domain`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<domain:name>`` **(1)** – the domain name as :term:`eppcom:labelType`,
* ``<domain:crDate>`` **(1)** – the :ref:`timestamp <mngobj-timestamps>` of creation as :term:`xs:dateTime`,
* ``<domain:exDate>`` **(0..1)** – the date of expiration as :term:`xs:date`.

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
            <domain:creData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>thisdomain.cz</domain:name>
               <domain:crDate>2017-08-09T12:31:49+02:00</domain:crDate>
               <domain:exDate>2018-08-09</domain:exDate>
            </domain:creData>
         </resData>
         <trID>
            <clTRID>zbdm002#17-08-09at12:31:47</clTRID>
            <svTRID>ReqID-0000141086</svTRID>
         </trID>
      </response>
   </epp>


ENUM extension
^^^^^^^^^^^^^^

:ref:`Response extension <response-ext>` is not used in reply to this command.
