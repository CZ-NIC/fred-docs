


Poll acknowledge
================

A poll acknowledge command is used to confirm that a message has been
received by the client and can be removed from the queue on the server.

The poll command is a ``poll`` element in the default namespace
(``urn:ietf:params:xml:ns:epp-1.0``).

.. index:: Ⓔpoll, ⓐop, ⓐmsgID

Command element structure
-------------------------

* ``<poll/>`` **(1)** as an empty element,
   * ``@op`` **(R)** poll operation; must equal ``ack`` to acknowledge the reading
     of the message,
   * ``@msgID`` identification number of the message to be confirmed;
     required with ``@op = 'ack'``;
     this is the current message identifier returned in :ref:`response to
     a poll request <struct-pollreq-response>`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <poll msgID="19596173" op="ack"/>
         <clTRID>cmmp003#17-07-21at11:21:41</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > poll ack 19596173

.. index:: ⒺmsgQ, ⓐcount, ⓐid

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the standard result, message queue and transaction identification.

See also :ref:`succ-fail`.

* ``<msgQ/>`` **(0..1)** – message queue info as an empty element; present only
  if there are some messages in the queue.

.. rubric:: Example

.. code-block:: xml

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
