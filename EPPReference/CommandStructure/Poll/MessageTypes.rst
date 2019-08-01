


Poll message types
==================

..
   FRED poll message types:

   * object-independent: ``<fred:lowCreditData>``, ``<fred:requestFeeInfoData>``,
   * domains: ``<domain:trnData>``, ``<domain:impendingExpData>``, ``<domain:expData>``,
     ``<domain:dnsOutageData>``, ``<domain:delData>``, ``<domain:updateData>``
     + ENUM: ``<enumval:impendingValExpData>``, ``<enumval:valExpData>``
   * contacts: ``<contact:trnData>``, ``<contact:idleDelData>``, ``<contact:updateData>``
   * nssets: ``<nsset:trnData>``, ``<nsset:idleDelData>``, ``<nsset:updateData>``, ``<nsset:testData>``
   * keysets: ``<keyset:trnData>``, ``<keyset:idleDelData>``, ``<keyset:updateData>``

.. Note:: The content of messages is not processed for validity,
   the markup has a formatting purpose.

.. contents::
   :local:
   :backlinks: none

.. index:: ⒺlowCreditData, Ⓔzone, Ⓔlimit, Ⓔcredit

.. _epp-poll-type-low-credit:

Low credit
----------

**Event:** Client's credit has dropped below the stated limit.

``<fred:lowCreditData>`` **(1)** declares the ``fred`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contains:

* ``<fred:zone>`` **(1)** – FQDN of the zone in question as :term:`eppcom:labelType`,
* ``<fred:limit>`` **(1)** – the stated limit:
   * ``<fred:zone>`` **(1)** – zone as :term:`eppcom:labelType`,
   * ``<fred:credit>`` **(1)** – credit treshold for notice as :term:`fred:amountType`,
* ``<fred:credit>`` **(1)** – amount of credit:
   * ``<fred:zone>`` **(1)** – zone as :term:`eppcom:labelType`,
   * ``<fred:credit>`` **(1)** – current client's credit as :term:`fred:amountType`.

.. code-block:: xml
   :caption: Example of a notice of low credit

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19681433">
            <qDate>2017-07-25T15:03:43+02:00</qDate>
            <msg>
               <fred:lowCreditData xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.0.xsd">
                  <fred:zone>cz</fred:zone>
                  <fred:limit>
                     <fred:zone>cz</fred:zone>
                     <fred:credit>5000.00</fred:credit>
                  </fred:limit>
                  <fred:credit>
                     <fred:zone>cz</fred:zone>
                     <fred:credit>4999.00</fred:credit>
                  </fred:credit>
               </fred:lowCreditData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>fwpn006#17-07-25at16:04:34</clTRID>
            <svTRID>ReqID-0000140888</svTRID>
         </trID>
      </response>
   </epp>

.. index:: ⒺrequestFeeInfoData, ⒺperiodFrom, ⒺperiodTo, ⒺtotalFreeCount,
   ⒺusedCount, Ⓔprice

.. _epp-poll-type-request-usage:

Request usage
-------------

**Event:** Daily report of how many free requests have been made this month
so far, and how much the client will be charged for the requests
that exceed the limit.

``<fred:requestFeeInfoData>`` **(1)** declares the ``fred`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contains:

* ``<fred:periodFrom>`` **(1)** – the :ref:`timestamp <mngobj-timestamps>`
  of the start of the period as :term:`xs:dateTime`,
* ``<fred:periodTo>`` **(1)** – the :ref:`timestamp <mngobj-timestamps>`
  of the end of the period as :term:`xs:dateTime`,
* ``<fred:totalFreeCount>`` **(1)** – the amount of free requests (the limit)
  for this month as :term:`xs:unsignedLong`,
* ``<fred:usedCount>`` **(1)** – the total of requests used during the period
  as :term:`xs:unsignedLong`,
* ``<fred:price>`` **(1)** – additional charge for requests over the limit
  that the client will be billed as :term:`fred:amountType`.

.. code-block:: xml
   :caption: Example of a message about request usage

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19690926">
            <qDate>2017-07-27T01:15:10+02:00</qDate>
            <msg>
               <fred:requestFeeInfoData xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5">
                  <fred:periodFrom>2017-07-01T00:00:00+02:00</fred:periodFrom>
                  <fred:periodTo>2017-07-26T23:59:59+02:00</fred:periodTo>
                  <fred:totalFreeCount>25000</fred:totalFreeCount>
                  <fred:usedCount>243</fred:usedCount>
                  <fred:price>0.00</fred:price>
               </fred:requestFeeInfoData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>twnx002#17-07-27at12:10:13</clTRID>
            <svTRID>ReqID-0000140940</svTRID>
         </trID>
      </response>
   </epp>

.. index:: ⒺimpendingExpData, ⒺexpData, ⒺdnsOutageData, ⒺdelData,
   Ⓔname, ⒺexDate

.. _epp-poll-type-domain-exp:

Domain expiration
-----------------

There are several messages concerning expiration of domains
that have the same content but are issued on different **events**:

* ``<domain:impendingExpData>`` – the domain is going to expire
  (see :ref:`expW state <registration-expiration>`),
* ``<domain:expData>`` – the domain has :ref:`expired <registration-expiration>`,
* ``<domain:dnsOutageData>`` – the domain has become :ref:`unguarded
  <registration-expiration>` and has been excluded from the zone,
* ``<domain:delData>`` – the domain has been :ref:`deleted <registration-expiration>`
  after registration expiration.

Only one of these elements can occur in a single poll message.

All of these elements declare the ``domain`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`,
and contain the following child elements:

* ``<domain:name>`` **(1)** – the domain name they are referring to
  as :term:`eppcom:labelType`,
* ``<domain:exDate>`` **(1)** – the expiration date of the domain name
  as :term:`xs:date`.

.. code-block:: xml
   :caption: Example of a message about impending domain expiration

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19690946">
            <qDate>2017-07-27T12:13:55+02:00</qDate>
            <msg>
               <domain:impendingExpData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
                  <domain:name>somedomain.cz</domain:name>
                  <domain:exDate>2017-08-26</domain:exDate>
               </domain:impendingExpData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>lelg003#17-07-27at12:42:33</clTRID>
            <svTRID>ReqID-0000140944</svTRID>
         </trID>
      </response>
   </epp>

.. index:: ⒺimpendingValExpData, ⒺvalExpData, Ⓔname, ⒺvalExDate

.. _epp-poll-type-domain-val:

ENUM domain validation
----------------------

Messages concerning the validation of ENUM domains for **events**:

* ``<enumval:impendingValExpData>`` – domain's validation is going to expire
  (see :ref:`valW1 state <validation-expiration>`),
* ``<enumval:valExpData>`` – domain's validation has expired (see :ref:`notValidated
  state <validation-expiration>`).

Only one of these elements can occur in a single poll message.

Both of these elements declare the ``enumval`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contain the same child elements:

* ``<enumval:name>`` **(1)** – the domain name to which they are referring
  as :term:`eppcom:labelType`,
* ``<enumval:valExDate>`` **(1)** – the expiration date of domain validation
  as :term:`xs:date`.

.. code-block:: xml
   :caption: Example of a message about ENUM validation expiration

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19847350">
            <qDate>2017-08-14T13:19:29+02:00</qDate>
            <msg>
               <enumval:impendingValExpData xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.0.xsd">
                  <enumval:name>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</enumval:name>
                  <enumval:valExDate>2017-08-15</enumval:valExDate>
               </enumval:impendingValExpData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>fmvu002#17-08-14at13:23:05</clTRID>
            <svTRID>ReqID-0000141213</svTRID>
         </trID>
      </response>
   </epp>

.. index:: ⒺtrnData, Ⓔname, Ⓔid, ⒺclID

.. _epp-poll-type-transfer:

Object transfer
---------------

**Event:** An object has been transferred to another registrar.

This message type appears in all 4 object namespaces: ``domain``, ``contact``,
``nsset``, ``keyset``.

``<*:trnData>`` **(1)** declares the object :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contains:

* an object identifier **(1)** which is **one of**:
   * ``<domain:name>`` – a domain name as :term:`eppcom:labelType`,
   * ``<*:id>`` – an object handle as :term:`fredcom:objIDType` (for objects
     other than domains),
* ``<*:trDate>`` **(1)** – the date of the transfer as :term:`xs:dateTime`,
* ``<*:clID>`` **(1)** – the handle of the registrar who requested the transfer
  as :term:`eppcom:clIDType`.

.. code-block:: xml
   :caption: Example of a transfer message

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19681434">
            <qDate>2017-07-25T16:34:42+02:00</qDate>
            <msg>
               <domain:trnData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
                  <domain:name>trdomain.cz</domain:name>
                  <domain:trDate>2017-07-25</domain:trDate>
                  <domain:clID>REG-FRED_A</domain:clID>
               </domain:trnData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>qfja002#17-07-25at16:39:03</clTRID>
            <svTRID>ReqID-0000140900</svTRID>
         </trID>
      </response>
   </epp>

.. index:: ⒺupdateData, ⒺopTRID, ⒺoldData, ⒺnewData

.. _epp-poll-type-update:

Object update
---------------

**Event:** An object has been updated by the Registry.

This message type appears in the following object namespaces: ``domain``,
``contact``, ``nsset``, ``keyset``.

``<*:updateData>`` **(1)** declares the object :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contains:

* ``<*:opTRID>`` **(1)** – operation transaction identifier (an identification
  of the operation in the Registry that has caused this message)
  as :term:`domain:trIDStringType`,
* ``<*:oldData>`` **(1)** – data before the update, the content is presented
  as an ``infData`` element (the same as in response to the ``info`` command:
  :ref:`domain:infData <domain-infdata>`,
  :ref:`contact:infData <contact-infdata>`,
  :ref:`nsset:infData <nsset-infdata>`,
  :ref:`keyset:infData <keyset-infdata>`),
* ``<*:newData>`` **(1)** – data after the update, the content is presented
  as an ``infData`` element (the same as in response to the ``info`` command:
  :ref:`domain:infData <domain-infdata>`,
  :ref:`contact:infData <contact-infdata>`,
  :ref:`nsset:infData <nsset-infdata>`,
  :ref:`keyset:infData <keyset-infdata>`).

.. code-block:: xml
   :caption: Example of a message about a domain update

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19852593">
            <qDate>2017-08-14T13:29:06+02:00</qDate>
            <msg>
               <domain:updateData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
                  <domain:opTRID>ReqID-0000141228</domain:opTRID>
                  <domain:oldData>
                     <domain:infData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                      xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
                        <domain:name>mydomain.cz</domain:name>
                        <domain:roid>D0009907597-CZ</domain:roid>
                        <domain:status s="serverBlocked">Domain blocked</domain:status>
                        <domain:status s="serverDeleteProhibited">Deletion forbidden</domain:status>
                        <domain:status s="serverRenewProhibited">Registration renewal forbidden</domain:status>
                        <domain:status s="serverRegistrantChangeProhibited">Registrant change forbidden</domain:status>
                        <domain:status s="serverTransferProhibited">Sponsoring registrar change forbidden</domain:status>
                        <domain:status s="serverUpdateProhibited">Update forbidden</domain:status>
                        <domain:registrant>CID-MYOWN</domain:registrant>
                        <domain:admin>CID-ADMIN1</domain:admin>
                        <domain:admin>CID-ADMIN2</domain:admin>
                        <domain:nsset>NID-MYNSSET</domain:nsset>
                        <domain:clID>REG-MYREG</domain:clID>
                        <domain:crID>REG-MYREG</domain:crID>
                        <domain:crDate>2017-07-11T13:28:48+02:00</domain:crDate>
                        <domain:upID>REG-FRED_C</domain:upID>
                        <domain:upDate>2017-08-11T10:46:14+02:00</domain:upDate>
                        <domain:exDate>2020-07-11</domain:exDate>
                        <domain:authInfo>rvBcaTVq</domain:authInfo>
                     </domain:infData>
                  </domain:oldData>
                  <domain:newData>
                     <domain:infData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                      xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
                        <domain:name>mydomain.cz</domain:name>
                        <domain:roid>D0009907597-CZ</domain:roid>
                        <domain:status s="serverBlocked">Domain blocked</domain:status>
                        <domain:status s="serverDeleteProhibited">Deletion forbidden</domain:status>
                        <domain:status s="serverRenewProhibited">Registration renewal forbidden</domain:status>
                        <domain:status s="serverRegistrantChangeProhibited">Registrant change forbidden</domain:status>
                        <domain:status s="serverTransferProhibited">Sponsoring registrar change forbidden</domain:status>
                        <domain:status s="serverUpdateProhibited">Update forbidden</domain:status>
                        <domain:registrant>CID-MYCONTACT</domain:registrant>
                        <domain:admin>CID-ADMIN1</domain:admin>
                        <domain:admin>CID-ADMIN2</domain:admin>
                        <domain:nsset>NID-MYNSSET</domain:nsset>
                        <domain:clID>REG-MYREG</domain:clID>
                        <domain:crID>REG-MYREG</domain:crID>
                        <domain:crDate>2017-07-11T13:28:48+02:00</domain:crDate>
                        <domain:upID>REG-CZNIC</domain:upID>
                        <domain:upDate>2017-08-14T13:29:06+02:00</domain:upDate>
                        <domain:exDate>2020-07-11</domain:exDate>
                        <domain:authInfo>rvBcaTVq</domain:authInfo>
                     </domain:infData>
                  </domain:newData>
               </domain:updateData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>fmvu004#17-08-14at13:29:27</clTRID>
            <svTRID>ReqID-0000141230</svTRID>
         </trID>
      </response>
   </epp>

.. code-block:: xml
   :caption: Example of a message about a contact update
   :name: contact-update-example

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
       <response>
           <result code="1301">
               <msg>Command completed successfully; ack to dequeue</msg>
           </result>
           <msgQ count="1" id="24024414">
               <qDate>2019-07-31T15:36:17+02:00</qDate>
               <msg>
                   <contact:updateData xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
                    xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.1.xsd">
                       <contact:opTRID>ReqID-0001071557</contact:opTRID>
                       <contact:oldData>
                           <contact:infData xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
                            xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.1.xsd">
                               <contact:id>TEST-POLL</contact:id>
                               <contact:roid>C0011364592-CZ</contact:roid>
                               <contact:status s="linked">Has relation to other records in the registry</contact:status>
                               <contact:postalInfo>
                                   <contact:name>Jan Novak</contact:name>
                                   <contact:addr>
                                       <contact:street>Narodni trida 1230/12</contact:street>
                                       <contact:city>Praha</contact:city>
                                       <contact:pc>12000</contact:pc>
                                       <contact:cc>CZ</contact:cc>
                                   </contact:addr>
                               </contact:postalInfo>
                               <contact:voice>+420.606000048</contact:voice>
                               <contact:email>primary@nic.cz</contact:email>
                               <contact:clID>REG-FRED_A</contact:clID>
                               <contact:crID>REG-FRED_A</contact:crID>
                               <contact:crDate>2019-07-31T15:34:15+02:00</contact:crDate>
                               <contact:disclose flag="1">
                                   <contact:addr/>
                               </contact:disclose>
                               <contact:ident type="birthday">1990-06-06</contact:ident>
                           </contact:infData>
                       </contact:oldData>
                       <contact:newData>
                           <contact:infData xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
                            xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.1.xsd">
                               <contact:id>TEST-POLL</contact:id>
                               <contact:roid>C0011364592-CZ</contact:roid>
                               <contact:status s="linked">Has relation to other records in the registry</contact:status>
                               <contact:postalInfo>
                                   <contact:name>Zmena Jmena</contact:name>
                                   <contact:addr>
                                       <contact:street>Nova adresa 2</contact:street>
                                       <contact:street>Nova druha adresa</contact:street>
                                       <contact:city>Nove Mesto</contact:city>
                                       <contact:pc>143 11</contact:pc>
                                       <contact:cc>CZ</contact:cc>
                                   </contact:addr>
                               </contact:postalInfo>
                               <contact:voice>+420.606000048</contact:voice>
                               <contact:email>primary@nic.cz</contact:email>
                               <contact:clID>REG-FRED_A</contact:clID>
                               <contact:crID>REG-FRED_A</contact:crID>
                               <contact:crDate>2019-07-31T15:34:15+02:00</contact:crDate>
                               <contact:upID>REG-FRED_A</contact:upID>
                               <contact:upDate>2019-07-31T15:36:17+02:00</contact:upDate>
                               <contact:disclose flag="1">
                                   <contact:addr/>
                               </contact:disclose>
                               <contact:ident type="birthday">1990-06-06</contact:ident>
                           </contact:infData>
                       </contact:newData>
                   </contact:updateData>
               </msg>
           </msgQ>
           <trID>
               <clTRID>rtjr004#19-07-31at15:36:22</clTRID>
               <svTRID>ReqID-0001071558</svTRID>
           </trID>
       </response>
   </epp>

.. index:: ⒺidleDelData, Ⓔid

.. _epp-poll-type-idle-del:

Idle object deletion
--------------------

**Event:** An object has been deleted because it had become :doc:`obsolete
</Concepts/LifeCycle/NonDomains>`.

This message type appears in the following object namespaces: ``contact``,
``nsset``, ``keyset``.

``<*:idleDelData>`` **(1)** declares the object :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`,
and contains:

* ``<*:id>`` **(1)** – the handle of the deleted object as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example of a message about a deleted idle object

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="19689674">
            <qDate>2017-07-26T18:28:55+02:00</qDate>
            <msg>
               <contact:idleDelData xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
                  <contact:id>CID-IDLE</contact:id>
               </contact:idleDelData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>cjtp007#17-07-26at18:30:02</clTRID>
            <svTRID>ReqID-0000140927</svTRID>
         </trID>
      </response>
   </epp>

.. index:: ⒺdelData, Ⓔname, ⒺexDate

.. _epp-poll-type-del:

Domain deletion
--------------------

**Event:** A domain has been deleted by the Registry for another reason than expiration.

``<domain:delData>`` **(1)** declares the object :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contains:

* ``<domain:name>`` **(1)** – the handle of the deleted object as :term:`eppcom:labelType`,
* ``<domain:exDate>`` **(1)** – the date of deletion as :term:`xs:date`.

.. Note:: This message type has the same content as domain deletion
   in :ref:`epp-poll-type-domain-exp`.

.. code-block:: xml
   :caption: Example of a message about a deleted domain

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="1" id="24115160">
            <qDate>2019-07-30T14:43:20+02:00</qDate>
            <msg>
                <domain:delData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
                 xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.1.xsd">
                    <domain:name>example.cz</domain:name>
                    <domain:exDate>2019-07-30</domain:exDate>
                </domain:delData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>budt002#19-07-30at14:48:59</clTRID>
            <svTRID>ReqID-0001043237</svTRID>
         </trID>
      </response>
   </epp>


.. index:: ⒺtestData, Ⓔid, Ⓔname, Ⓔresult, Ⓔtestname, Ⓔstatus, Ⓔnote

.. _epp-poll-type-techcheck:

Technical check results
-----------------------

**Event:** A technical check that the client had requested, has finished.

``<nsset:testData>`` **(1)** declares the ``nsset`` :doc:`namespace and schema
</EPPReference/SchemasNamespaces/index>`, and contains:

.. * ``<nsset:cltestid>`` **(0..1)** – clTRID of the tec.check request???
     as :term:`nsset:trIDStringType`, // probably unused

* ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:name>`` **(0..n)** – a listing of additional domain names that have
  been tested with the nsset as :term:`eppcom:labelType`,
* ``<nsset:result>`` **(0..n)** – the result of a single test:
   * ``<nsset:testname>`` **(1)** – the name of the test as :term:`eppcom:labelType`,
   * ``<nsset:status>`` **(1)** – success of the test as :term:`xs:boolean`:
     ``true`` – passed, ``false`` – failed,
   * ``<nsset:note>`` **(0..1)** – extended information about the result
     from the test implementation as :term:`xs:string`.

.. code-block:: xml
   :caption: Example of a message with the results of a technical check

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="2" id="19673434">
            <qDate>2017-07-24T17:33:43+02:00</qDate>
            <msg>
               <nsset:testData xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.2.xsd">
                  <nsset:id>NID-MYNSSET</nsset:id>
                  <nsset:name>'mydomain.cz'</nsset:name>
                  <nsset:result>
                     <nsset:testname>glue_ok</nsset:testname>
                     <nsset:status>true</nsset:status>
                  </nsset:result>
                  <nsset:result>
                     <nsset:testname>existence</nsset:testname>
                     <nsset:status>false</nsset:status>
                  </nsset:result>
               </nsset:testData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>yxak006#17-07-25at12:10:05</clTRID>
            <svTRID>ReqID-0000140877</svTRID>
         </trID>
      </response>
   </epp>
