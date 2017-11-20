
.. _FRED-EPPRef-Basics:

Protocol basics
===============

Extensible Provisioning Protocol (EPP) is an application-layer client-server
protocol which was designed for the provisioning and management of objects
stored in a shared central repository. It is a standard (:rfc:`5730`)
that is usually chosen
for communication between registrars (clients) and a domain registry (server).
The standard allows the protocol to be extended by providing an extension framework
which is used extensively in the FRED EPP implementation.

Communication between a client and the EPP server is performed
as an exchange of XML documents (further referred to as *messages*)
whose structure and content are defined by a :doc:`series of schemas
<../SchemasNamespaces/index>`.
EPP takes advantage of XML namespaces which make extensions easy.

.. _FRED-EPPRef-Basics-class:

A message sent from a client to the server is called a *request message*
which the server answers with what is called a *reply message*.

XML messages are transported over the Transmission
Control Protocol (TCP) with Transport Layer Security (TLS)
using a client's certificate. (See also :rfc:`5734`.)

.. NOTE A hash of the client certificate must be provided in the Registry.
   (for login)

.. rubric:: Chapter TOC

.. toctree::

   IntroEPP
   GenericMessage
   ServiceDiscovery
   Commands
   ProtocolExtensions
   ComResExtensions
