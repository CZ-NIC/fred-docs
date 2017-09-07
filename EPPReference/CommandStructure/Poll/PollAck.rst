


Poll acknowledgement
====================

A poll acknowledgement :ref:`command <struct-command>` is used to confirm
that a message has been received by the client and can be removed
from the queue on the server.

The poll command is a ``poll`` element in the default namespace
(``urn:ietf:params:xml:ns:epp-1.0``).

.. index:: Ⓔpoll, ⓐop, ⓐmsgID

Command element structure
-------------------------

The ``<poll/>`` **(1)** element must be empty and contain only attributes:

* ``@op`` **(R)** – poll operation; must equal ``ack`` to acknowledge the reading
  of the message,
* ``@msgID`` – the identification number of a message to be confirmed
  as :term:`eppcom:minTokenType`; required with ``@op = 'ack'``;
  this is the current message identifier returned in :ref:`response to
  a poll request <struct-pollreq-response>`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <poll msgID="19596173" op="ack"/>
         <clTRID>cmmp003#17-07-21at11:21:41</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > poll ack 19596173

.. index:: ⒺmsgQ, ⓐcount, ⓐid

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, message queue information and transaction identification.

See also :ref:`succ-fail`.

Structure of message queue information:

* ``<msgQ/>`` **(0..1)** – message queue information as an empty element;
  present only if there are some messages in the queue,

   * ``@count`` **(R)** – the count of messages in the queue
     as :term:`xs:unsignedLong`,
   * ``@id`` **(R)** – the identification number of the first message
     in the queue as :term:`eppcom:minTokenType`.

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
         <msgQ count="6" id="19603978"/>
         <trID>
            <clTRID>cmmp003#17-07-21at11:21:41</clTRID>
            <svTRID>ReqID-0000140401</svTRID>
         </trID>
      </response>
   </epp>
