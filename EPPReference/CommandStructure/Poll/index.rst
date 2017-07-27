
.. index:: poll

Polling
=======

Polling is used by the client to manage notifications about relevant events
in the Registry.

First, the client orders the notification messages by issuing a poll request.
In response, the server informs about the status of the message queue
(the message count), includes contents of the first (oldest) message
and provides its identifier for acknowledgement.

Then the client is supposed to confirm the receipt of this message by issuing
a poll acknowledgement with the identifier of the read message.
The server removes the acknowledged message from the message queue and responds
with a new message count and the identification of the next message in the queue.

The process can be repeated to read the remaining messages until the count is
reduced to zero.

.. ??? does FRED EPP server provide msgQ for other commands than poll? No.

.. toctree::

   PollReq
   PollAck
   MessageTypes
