
.. index:: poll, notification

Polling
=======

Polling is used by the client to manage notifications about relevant events
in the Registry.

The relevant events are mostly those that are not triggered by the client,
such as time-based events (expiration, deletion of idle objects),
asynchronous responses (technical check results),
events that are triggered by other registrars (transfer)
or by the Registry itself (consequences of contacts' merger).

The workflow is following:

#. The client orders the notification messages by issuing a poll request.

#. In response, the server informs about the status of the message queue
   (the message count), includes contents of the first (oldest) message
   and provides its identifier for acknowledgement.

#. The client is supposed to confirm the receipt of this message by issuing
   a poll acknowledgement with the identifier of the read message.

#. The server removes the acknowledged message from the message queue and responds
   with a new message count and the identification of the next message in the queue.

#. The previous steps can be repeated to read the remaining messages
   until the count is reduced to zero.

.. Note:: The EPP standard allows to announce a non-empty message queue
   (``<msgQ>``) in response to any command, however the FRED EPP server gives
   such response exclusively to an explicit poll request.

.. toctree::

   PollReq
   PollAck
   MessageTypes
