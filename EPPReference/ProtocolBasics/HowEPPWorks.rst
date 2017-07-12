
.. _FRED-EPPRef-Basics-HowEPPWorks:

How EPP works
=============

This section introduces the basic service aspects of the EPP,
describes the activities of normal communication between a client and
the EPP server and explains in general how FRED extends the standard protocol.

.. rubric:: Service aspects

EPP has the following basic service aspects:

* service discovery,
* commands & responses, and
* an extension framework.

*Service discovery* allows a client to be aware of managed objects,
supported services, extensions and policy of the EPP server.

*Commands* are used by a client either to establish and to end a session,
or to request standard operations over objects managed in the registry
to which the server replies with a coordinated
*response* containing the result of the requested operation.

The *extension framework* allows the protocol to be extended on several levels:

* *command-level* extensions – extensions of standard commands & responses,
* *object-level* extensions – object extensions with definitions of managed
  objects and relationship of protocol requests and replies to those objects,
* *protocol-level* extensions – protocol extensions with non-standard requests
  (such as new commands).

The FRED extends the EPP on all three levels as described below.

.. rubric:: Normal communication

The normal communication between a client and the EPP server will be:

* Client connects to server over TCP+TLS.
* Server identifies itself and the commands and extensions that it supports.
  (Sends the ``greeting``.)
* Client logs in by supplying login name, password and session options.
* Client issues commands to server, which then replies immediately
  with a result.
* Client then idles until it has more commands to send, polling periodically
  for any notifications.
* Client logs out (or times out).

.. _fig-epp-conversation:

.. figure:: ../_graphics/conversation.png
   :alt: EPP conversation sequence diagram
   :align: center

   Sequence diagram – A normal EPP communication



.. rubric:: Use of the extension framework in FRED EPP

* :doc:`protocol-level extensions <ProtocolExtensions>` (custom commands)
   * xpath ``/epp/extension/*:*``
   * listings
   * creditInfo
   * sendAuthInfo, test
* :doc:`object-level extensions <ManagedObjects>` (custom managed objects)
   * xpath ``/epp/command/{std-cmd}/{object}:{std-cmd}``
   * xpath ``/epp/extension/fred:extcommand/{object}:{ext-cmd}``
   * object attributes
   * command-response mapping
   * (sendAuthInfo, test)
* command/response-level extensions (additional attributes of ENUM domains)
   * :ref:`command extension <command-ext>` xpath ``/epp/command[{std-cmd}]/extension/*:*``
   * :ref:`response extension <response-ext>` xpath ``/epp/response[result]/extension/*:*``
