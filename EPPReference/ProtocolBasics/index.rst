
.. _FRED-EPPRef-Basics:

Protocol basics
===============

Extensible Provisioning Protocol (EPP) is an application-layer client-server
protocol which was designed for the provisioning and management of objects
stored in a shared central repository. It is a standard (:rfc:`5730`)
that is usually chosen
for communication between registrars (clients) and a domain registry (server).

The communication between a client and the EPP server is performed
as an exchange of XML documents (further referred to as *messages*)
whose structure and content are defined by a :doc:`series of schemas
<../SchemasNamespaces/index>`.
EPP takes advantage of XML namespaces which make extensions easy.

.. _FRED-EPPRef-Basics-class:

A message sent from a client to the server is called a *request message*
which the server answers with what is called a *reply message*.

.. rubric:: Transport & security

In the FRED implementation, XML messages are transported over the Transmission
Control Protocol (TCP) with Transport Layer Security (TLS)
using a client's certificate. (See also :rfc:`5734`.)

.. NOTE A hash of the client certificate must be provided in the Registry.
   (for login)

.. rubric:: General features of the EPP protocol

* EPP is a stateful protocol. (The server retains session information
  about each client.)
* All comunication is initiated by a client. (The server does not send anything
  to a client unless it was requested by the client.)
* The server responds to client-initiated communication (which
  can be either a TCP connection request or an EPP service
  discovery request (``hello``)) by returning a ``greeting`` to the client.
* The server responds to each EPP command with a coordinated response
  that describes the results of processing the command. (See also
  `EPP Server State Machine <https://tools.ietf.org/html/rfc5730#page-5>`_
  for a more detailed description of server's behaviour.)
* Commands are processed by the server in the order they are received
  from clients.
* Commands are atomic. (There is no partial success or partial failure.)
* The FRED EPP server does not allow delayed execution of commands (pending),
  commands are performed immediately.

.. * Commands are idempotent. (Executing a command more than once has the same
  net effect on object state as successfully executing the command once.)
  NOTE Some are not. (example?)

.. rubric:: Chapter TOC

.. toctree::

   HowEPPWorks
   GenericMessage
   ServiceDiscovery
   Commands
   ManagedObjects
   ProtocolExtensions
