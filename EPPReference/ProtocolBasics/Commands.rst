


Commands & responses
====================

A command is an :ref:`EPP request <FRED-EPPRef-Basics-class>`.

EPP commands fall into three categories: session management commands,
query commands, and object transform commands.

* *Session management commands* are used to establish and end persistent sessions
  with the EPP server.

* *Query commands* are used to perform read-only object information retrieval
  operations.

* *Transform commands* are used to perform read-write object management operations.

A response is an :ref:`EPP reply <FRED-EPPRef-Basics-class>` coordinated with the command.

The command-response pair is also called a **transaction**.
Transactions are always described together as a whole in this manual.


Implemented standard commands
-----------------------------

* Session management commands: login, logout

* Query commands: check, info, poll (``request`` and ``acknowledge`` operations)

* Transform commands: create, update, transfer (``request`` operation only), renew, delete

See also :doc:`command overview <../CommandStructure/index>` for implemented
non-standard (custom) commands,
or :doc:`ProtocolExtensions` for the generic syntax of custom commands.

.. Note:: The standard suggests a more complex handling of object transfer
   which is not applicable in the FRED. Therefore the other transfer operations
   (query, cancel, approve, reject) are not implemented in the FRED EPP.

.. index:: ⒺtrID, ⒺclTRID, ⒺsvTRID
   pair: transaction; identifier

.. _trans-ident:

Transaction identification
--------------------------

To make sure that both the client and the EPP server have consistent temporal
and state-management records, both commands and responses should be marked
with unique identifiers.

A **command** should be assigned a ``clTRID`` (client transaction identifier)
by the client which uniquely identifies the command to the client.
The client is supposed to maintain its own transaction identifier
space to ensure uniqueness. Also the format of the identifier is arbitrary
as long as it complies with the restrictions of the XML schema
(:term:`epp:trIDStringType`).

A **response** will be assigned by the server:

* the ``clTRID`` of the command for which the response is being returned
  *if provided by the client*,
* an additional ``svTRID`` (server transaction identifier)
  that marks this transaction from the server's perspective.

Transaction identifiers should be logged, retained and protected.

.. todo:: disable notification prefix

.. _struct-command:

Command element structure
--------------------------

The ``<command>`` element is a child of ``<epp>`` and is defined in the standard
EPP namespace. It contains a command type of object-related commands or
an actual object-independent command, also in the standard namespace,
which must be a **singular** occurrence of **one of** the following:

* ``<login>`` – client login (establish a session), an object-independent
  command, see :doc:`../CommandStructure/Login`,
* ``<logout>`` – client logout (end the session), an object-independent
  command, see :doc:`../CommandStructure/Logout`,
* ``<check>`` – object availability checks, an object-related command type,
* ``<create>`` – object registrations, an object-related command type,
* ``<delete>`` – object unregistrations, an object-related command type,
* ``<info>`` – requests for object details, an object-related command type,
* ``<renew>`` – object registration renewals (to be used only with domains), an object-related command type,
* ``<transfer>`` – object transfer requests, an object-related command type:
   * ``@op`` **(R)** – transfer operation –
     Because of :doc:`the concept of transfer </Concepts/Transfer>`
     in the FRED, only one value is permitted and that is ``request``
     which is used to request a transfer.
* ``<update>`` – updates of object details, an object-related command type,
* ``<poll>`` – polling for notifications from the Registry, an object-independent command, see :doc:`../CommandStructure/Poll/index`.
   * ``@op`` **(R)** – poll operation as one of values:
      * ``req`` – requests poll messages,
      * ``ack`` – acknowledges reading of a message,
   * ``@msgID`` – identifier of the message to be acknowledged
     as a :term:`xs:token`. Use only with ``@op = 'ack'``.

Each object-related command type may contain elements from any namespace.
This is where the namespaces and appropriate top-level elements of :doc:`managed
objects <../ManagedObjects/index>` come in. The object's top-level element must
correspond with the command type.

The command type may be followed by:

* ``<extension>`` **(0..1)** – command extension container (see :ref:`command-ext`),
* ``<clTRID>`` **(0..1)** – client :ref:`transaction identifier <trans-ident>`
  as :term:`epp:trIDStringType`.

.. code-block:: xml
   :caption: Example of a standard command

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <!-- Command container -->
      <command>
         <!-- Command type: info, check, create, delete... -->
         <info>
            <!-- Command arguments container -->
            <object:info>
               <!-- Object-defined content -->
            </object:info>
         </info>
         <!-- Client transaction identifier -->
         <clTRID>fyyp004#17-05-30at13:02:36</clTRID>
      </command>
   </epp>

Command contents are described separately for each justified combination
of a command type and a managed object.

.. _struct-response:

Response element structure
--------------------------

The ``<response>`` element is a child of ``<epp>`` and is defined in the standard
EPP namespace. It contains the following child elements:

* ``<result>`` **(1..n)** – report of the :ref:`success or failure of command <succ-fail>` execution:
   * ``@code`` **(R)** – result code (4-digit number), for a list of possible
     values see :doc:`result codes </EPPReference/Appendixes/ResultCodes>`,
   * ``<msg>`` **(1)** – human-readable description of the result,
      * ``@lang`` – language of the result description
        as :term:`xs:language`; default is ``en`` (English),
   * ``<value>`` **(0..n)** – identification of a client-provided element
     or other information that caused a server error condition,
   * ``<extValue>`` **(0..n)** – additional error diagnostic information:
      * ``<value>`` **(1)** – identification of a client-provided element
        or other information that caused a server error condition,
      * ``<reason>`` **(1)** – human readable message that describes the reason
        for the error (see :doc:`/EPPReference/Appendixes/ErrorReasons` for a complete list),

         * ``@lang`` – language of the reason description
           as :term:`xs:language`; default is ``en`` (English),

* ``<msgQ>`` **(0..1)** – description of queued poll messages; in the FRED EPP,
  this element is present only in a response to a ``poll`` command,
  for detailed syntax and usage see :doc:`../CommandStructure/Poll/index`,
* ``<resData>`` **(0..1)** – response data element that contains child elements
  specific to the command and/or associated object,
* ``<extension>`` **(0..1)** – response extension container, see :ref:`response-ext`,
* ``<trID>`` **(1)** – :ref:`transaction identifier <trans-ident>` composed of:
   * ``<clTRID>`` **(0..1)** – client transaction identifier,
   * ``<svTRID>`` **(1)** – server transaction identifier.

.. code-block:: xml
   :caption: Example of a response (successful execution)

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <!-- Response container -->
      <response>
         <!-- Result code and message -->
         <result code="1000">
            <msg>Command completed successfully</msg>
         </result>
         <!-- Response data -->
         <resData>
            <!-- Data container -->
            <object:someData xmlns:object="object:namespace:id"
             xsi:schemaLocation="object:namespace:id path/to/schema.xsd">
               <!-- Object-defined content -->
            </object:someData>
         </resData>
         <!-- Transaction identification -->
         <trID>
            <clTRID>fyyp004#17-05-30at13:02:36</clTRID>
            <svTRID>ReqID-0000135148</svTRID>
         </trID>
      </response>
   </epp>

.. _plain-result:

.. Note::

   .. rubric:: Plain result message

   A response is called a "plain result message" when it contains only
   the result (``<result>``) and transaction identification (``<trID>``)
   and nothing else. The result can be either a success or failure.

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
            <trID>
               <clTRID>sdmj001#17-03-06at18:48:03</clTRID>
               <svTRID>ReqID-0000126633</svTRID>
            </trID>
         </response>
      </epp>

.. _succ-fail:

Success or failure of a command
-------------------------------

A response always contains the result of executing the command and each result
is described by both a code and a textual message.

If the execution succeeded, a code of 1xxx series is returned.
If the execution failed, a code of 2xxx series is returned.
See :doc:`/EPPReference/Appendixes/ResultCodes` for an overview.

The standard allows to return several results, but the FRED EPP server
returns exactly one result at a time.

.. Important:: The **response element structure** of specific commands is
   described only for cases when the execution is **successful** and therefore
   it is expected that it may contain some response data, depending on the command.

.. code-block:: xml
   :caption: Example of a response (failure)

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="2306">
            <msg>Parameter value policy error</msg>
            <extValue>
               <value>
                  <nsset:tech xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2">C12-58326</nsset:tech>
               </value>
               <reason>Duplicity contact</reason>
            </extValue>
            <extValue>
               <value>
                  <nsset:tech xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2">C17-58326</nsset:tech>
               </value>
               <reason>Duplicity contact</reason>
            </extValue>
         </result>
         <trID>
            <clTRID>znmw008#17-08-11at16:20:05</clTRID>
            <svTRID>ReqID-0000512432</svTRID>
         </trID>
      </response>
   </epp>
