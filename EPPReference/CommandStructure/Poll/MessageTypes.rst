


Poll message types
==================

FRED poll message types:

* object-independent: ``<fred:lowCreditData>``, ``<fred:requestFeeInfoData>``,
* domains: ``<domain:trnData>``, ``<domain:impendingExpData>``, ``<domain:expData>``,
  ``<domain:dnsOutageData>``, ``<domain:delData>``, ``<domain:updateData>``
  + ENUM: ``<enumval:impendingValExpData>``, ``<enumval:valExpData>``
* contacts: ``<contact:trnData>``, ``<contact:idleDelData>``, ``<contact:updateData>``
* nssets: ``<nsset:trnData>``, ``<nsset:idleDelData>``, ``<nsset:updateData>``, ``<nsset:testData>``
* keysets: ``<keyset:trnData>``, ``<keyset:idleDelData>``, ``<keyset:updateData>``


.. contents::
   :local:

Low credit
----------

**Event:** Client's credit has dropped below the stated limit.

``<fred:lowCreditData>`` **(1)** declares the ``fred`` namespace and schema,
and contains:

* ``<fred:zone>`` **(1)** – FQDN of the zone in question as :term:`eppcom:labelType`,
* ``<fred:limit>`` **(1)** – the stated limit:
   * ``<fred:zone>`` **(1)** – zone as :term:`eppcom:labelType`,
   * ``<fred:credit>`` **(1)** – credit treshold for notification as :term:`fred:amountType`,
* ``<fred:credit>`` **(1)** – amount of credit:
   * ``<fred:zone>`` **(1)** – zone as :term:`eppcom:labelType`,
   * ``<fred:credit>`` **(1)** – current client's credit as :term:`fred:amountType`.

.. code-block:: xml
   :caption: Example of low credit notification

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

Request usage
-------------

**Event:** Daily report of how many requests of the prepaid amount have been
used this month so far, and how much the client will be charged for the requests
that exceed the prepaid amount.

``<fred:requestFeeInfoData>`` **(1)** declares the ``fred`` namespace and
schema, and contains:

* ``<fred:periodFrom>`` **(1)** – start of the period as :term:`xs:dateTime`,
* ``<fred:periodTo>`` **(1)** – end of the period as :term:`xs:dateTime`,
* ``<fred:totalFreeCount>`` **(1)** – the amount of prepaid requests (the limit)
  per month as :term:`xs:unsignedLong`,
* ``<fred:usedCount>`` **(1)** – the total of requests used during the period
  as :term:`xs:unsignedLong`,
* ``<fred:price>`` **(1)** – additional charge for requests over limit
  that the client will be billed as :term:`fred:amountType`.

.. code-block:: xml
   :caption: Example of a notification about the request usage

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



Domain life cycle
-----------------

There are several notifications concerning the life cycle of domains
that have the same content but are issued on different **events**:

* ``<domain:impendingExpData>`` – the domain is going to expire (by default 30 days before expiration),
* ``<domain:expData>`` – the domain has expired (on the date of expiration),
* ``<domain:dnsOutageData>`` – the domain has been excluded from the zone (by default 30 days after expiration),
* ``<domain:delData>`` – the domain has been deleted (by default 62 days after expiration or deleted by the Registry???).

Only one of these elements can occur in a single poll message.

All of these elements declare the ``domain`` namespace and schema,
and contain the following child elements:

* ``<domain:name>`` **(1)** – the domain name to which they are referring
  as :term:`eppcom:labelType`,
* ``<domain:exDate>`` **(1)** – the expiration date of the domain name
  as :term:`xs:date`.

.. code-block:: xml
   :caption: Example of a notification of impending domain expiration

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
                xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.1.xsd">
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



ENUM domain validation
----------------------

Notifications concerning the validation of ENUM domains for **events**:

* ``<enumval:impendingValExpData>`` – domain's validation is going to expire (by default X days before validation expiration),
* ``<enumval:valExpData>`` – domain's validation has expired (on the day of validation expiration).

Only one of these elements can occur in a single poll message.

Both of these elements declare the ``enumval`` namespace and schema,
and contain the same child elements:

* ``<enumval:name>`` **(1)** – the domain name to which they are referring
  as :term:`eppcom:labelType`,
* ``<enumval:valExDate>`` **(1)** – the expiration date of domain validation
  as :term:`xs:date`.



Object transfer
---------------

**Event:** An object has been transferred.

``<*:trnData>`` **(1)** declares the object namespace and schema,
and contains:

* an object identifier **(1)** which is **one of**:
   * ``<domain:name>`` – a domain name as :term:`eppcom:labelType`,
   * ``<*:id>`` – an object handle as :term:`fredcom:objIDType` (for objects
     other than domains),
* ``<*:trDate>`` **(1)** – the date of the transfer as :term:`xs:dateTime`,
* ``<*:clID>`` **(1)** – the handle of the registrar who requested the transfer
  as :term:`eppcom:clIDType`.

This message type appears in all 4 object namespaces: ``domain``, ``contact``, ``nsset``, ``keyset``.

.. code-block:: xml
   :caption: Example of transfer notification

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
                xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.1.xsd">
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



Object update
---------------

**Event:** An object has been updated.

``<*:updateData>`` **(1)** declares the object namespace and schema,
and contains:

* ``<*:opTRID>`` **(1)** – ??? as :term:`domain:trIDStringType`,
* ``<*:oldData>`` **(1)** – data before the update, contents same as info command resData...,
* ``<*:newData>`` **(1)** – data after the update, contents same as info command resData....

This message type appears in the following object namespaces: ``domain``, ``nsset``, ``keyset``.

Idle object deletion
--------------------

**Event:** An object has been deleted because it had not been used for a long time.

``<*:idleDelData>`` **(1)** declares the object namespace and schema,
and contains:

* ``<*:id>`` **(1)** – the handle of the deleted object as :term:`fredcom:objIDType`.

This message type appears in the following object namespaces: ``contact``, ``nsset``, ``keyset``.

.. code-block:: xml
   :caption: Example of a notification of a deleted idle object

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
                xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.1.xsd">
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



.. _struct-poll-test:

Technical check results
-----------------------

**Event:** A technical check that the client has requested, has finished.

``<nsset:testData>`` **(1)** declares the ``nsset`` namespace and schema,
and contains:

* ``<nsset:cltestid>`` **(0..1)** – ??? as :term:`nsset:trIDStringType`,
* ``<nsset:id>`` **(1)** – nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:name>`` **(0..n)** – a listing of domains that ??? as :term:`eppcom:labelType`,
* ``<nsset:result>`` **(0..n)** – the result of a single test:
   * ``<nsset:testname>`` **(1)** – the name of the test as :term:`eppcom:labelType`,
   * ``<nsset:status>`` **(1)** – success of the test as :term:`xs:boolean`:
     ``true`` – passed, ``false`` – failed,
   * ``<nsset:note>`` **(0..1)** – note ??? as :term:`xs:string`.

.. code-block:: xml
   :caption: Example of notification with the results of a technical check

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
                xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.1.xsd">
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
