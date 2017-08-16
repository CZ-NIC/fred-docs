


Poll request
=============

A poll request command is used to obtain the message queue status (message count)
and contents of the first message in the queue (the oldest one).

The poll command is a ``poll`` element in the default namespace
(``urn:ietf:params:xml:ns:epp-1.0``).

.. index:: Ⓔpoll, ⓐop

Command element structure
-------------------------

The ``<poll/>`` **(1)** element must be empty and contain only this attribute:

   * ``@op`` **(R)** poll operation; must equal ``req`` to make the request.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <poll op="req"/>
         <clTRID>cmmp002#17-07-21at11:19:09</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > poll req

.. index:: ⒺmsgQ, ⒺqDate, Ⓔmsg, ⓐcount, ⓐid, ⓐlang

.. _struct-pollreq-response:

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the standard result, message queue and transaction identification.

See also :ref:`succ-fail`.

Structure of the message queue:

* ``<msgQ>`` **(0..1)** – the message queue:
   * ``@count`` **(R)** – number of messages in the queue as :term:`xs:unsignedLong`,
   * ``@id`` **(R)** – current message identifier as :term:`eppcom:minTokenType`,
   * ``<qDate>`` **(0..1)** – the date and time that the message was enqueued
     as :term:`xs:dateTime`,
   * ``<msg>`` **(0..1)** – the container of the current message,
      * ``@lang`` – language of the message text as :term:`xs:language`;
        default is ``en`` (English),
      * **one of** the messages such as ``<fred:lowCreditData>``,
        ``<fred:requestFeeInfoData>`` or other, see :doc:`MessageTypes`.

     .. Note:: There is always just one message contained in the ``<msg>`` element.

        The content of the ``<msg>`` element is not processed for validity.



.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg>Command completed successfully; ack to dequeue</msg>
         </result>
         <msgQ count="7" id="19596173">
            <qDate>2017-07-15T01:18:13+02:00</qDate>
            <msg>
               <fred:requestFeeInfoData xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5">
                  <fred:periodFrom>2017-07-01T00:00:00+02:00</fred:periodFrom>
                  <fred:periodTo>2017-07-14T23:59:59+02:00</fred:periodTo>
                  <fred:totalFreeCount>25000</fred:totalFreeCount>
                  <fred:usedCount>120</fred:usedCount>
                  <fred:price>0.00</fred:price>
               </fred:requestFeeInfoData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>cmmp002#17-07-21at11:19:09</clTRID>
            <svTRID>ReqID-0000140400</svTRID>
         </trID>
      </response>
   </epp>
