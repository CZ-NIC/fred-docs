


EPP client workflow
===================

Registrars communicate with the registry through FRED's registrar interface,
which is based on the EPP and which the registrars use as clients.

There are 3 options for using the registrar interface:

* command-line Python client (supplied with the FRED),
* client Python API library (supplied with the FRED),
* registrar's custom client built on the raw EPP.

Although these three options vary in syntax, they have the same workflow,
since they all talk to the same EPP server. This chapter describes the general workflow,
which is independent from the syntax, while giving you hints about the syntax.

Of course, correct syntax is a necessary condition for the commands to be carried out.

Each EPP command allows you to append your own :ref:`client transaction identifier <trans-ident>`.

.. Note:: This chapter assumes that the client is a *regular* registrar
   (not the *system* registrar).

.. rubric:: Where to get detailed help with syntax

The CLI client has an embedded command help. It also allows you to enter the commands
in an interactive mode by filling in command parameters one by one, or enter the parameters
by their names.
See `Additional FRED-client abilities`_.

Python API methods have the same names as CLI client commands, they differ in parameter
syntax and order. You may view the API reference by starting the pydoc server ``pydoc -p 8080``
from the command line and then opening http://localhost:8080 in a browser.

The EPP syntax itself is described in detail in the :doc:`/EPPReference/index`.
This chapter will provide you with links to specific EPP-commands as you read on.



.. contents:: Chapter TOC
   :local:
   :backlinks: none

.. _epp-client-connect:

Connecting to the server
------------------------

The client must:

* create a secure socket using a public certificate and private key,
* connect via the socket to the EPP server using a hostname and port,
* once connected, start reading data coming from the EPP server.

When you use the raw EPP, you need to find your own way of connecting to the EPP
server, whereas the client programs will do it for you, all you need to do is supply
connection settings in a configuration file.

Detailed requirements for transfer over TCP are in :rfc:`5734`.

.. _epp-client-discover:

Getting service information
---------------------------

Once the client is connected to the server, the first data it receives contains the
:doc:`greeting </EPPReference/ProtocolBasics/ServiceDiscovery>`.

What might interest you in the greeting (:code:`xpath:/epp/greeting/`):

* protocol version (:code:`svcMenu/version`),
* service languages provided (:code:`svcMenu/lang`),
* namespaces of managed objects (:code:`svcMenu/objURI`),
* namespaces of service extensions (:code:`svcExtension/extURI`),
* description of the data collection policy (:code:`dcp`).

You actually need the first four items to establish a session.

To get the greeting, you just need to :ref:`connect to the EPP server <epp-client-connect>`
or send a :doc:`hello </EPPReference/ProtocolBasics/ServiceDiscovery>`.

.. _epp-client-login:

Establishing a session (login)
------------------------------

This is the first command you must issue.

To login, you send the ``login`` command (:ref:`display help <epp-client-help>`
/ :doc:`see the reference </EPPReference/CommandStructure/Login>`)
with a username, password and, eventually, other session settings,
such as the interface language.

The CLI client can use configuration settings to login automatically
when it is launched. It requests use of all namespaces automatically.

Once you are logged in, you may start issuing other commands.

.. _epp-client-registering:

Registering domains & other objects
-----------------------------------

In a nutshell, if you're a newcomer without previous records, you must proceed
with registrations in this order:

#. :ref:`Login <epp-client-login>`, before you begin.
#. :ref:`Check <epp-client-check>` that an object can be registered.
#. :ref:`Create a contact <epp-client-create-contact>`.
#. Optionally, :ref:`create an nsset <epp-client-create-nsset>` (using a contact).
#. Optionally, :ref:`create a keyset <epp-client-create-keyset>` (using a contact).
#. :ref:`Create a domain <epp-client-create-domain>` (using a contact, and optionally an nsset and keyset).


.. _epp-client-check:

Check domain names and handles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When registering a new object of any type, you need to name it
with a **unique identifier** -- a domain name or a handle.
In case of domain names, the holders choose them for themselves of course.
But for the other objects, it is you who names them. To make sure that a domain
name or handle can be registered,
use a ``check`` command according to the object type:

* ``check_domain`` (:ref:`display help <epp-client-help>`)
  / ``domain:check`` (:doc:`see the reference </EPPReference/CommandStructure/Check/CheckDomain>`),
* ``check_contact`` (:ref:`display help <epp-client-help>`)
  / ``contact:check`` (:doc:`see the reference </EPPReference/CommandStructure/Check/CheckContact>`),
* ``check_nsset`` (:ref:`display help <epp-client-help>`)
  / ``nsset:check`` (:doc:`see the reference </EPPReference/CommandStructure/Check/CheckNsset>`),
* ``check_keyset`` (:ref:`display help <epp-client-help>`)
  / ``keyset:check`` (:doc:`see the reference </EPPReference/CommandStructure/Check/CheckKeyset>`).

The command will tell you not only whether an object has not been registered yet,
but also whether the name/handle has correct syntax and is acceptable by the Registry.

Formats for domain names and handles are properly described in the chapter
:doc:`/EPPReference/ManagedObjects/Common` (EPP Reference).

You may also check several objects of the same type with one call,
because the commands accept multiple parameters.

.. _epp-client-create-contact:

Create a contact
^^^^^^^^^^^^^^^^

To register a domain name, you must first record personal information, to which the domain name
will be linked. Personal information is recorded using :doc:`contact objects
</EPPReference/ManagedObjects/Contacts>`, which hold information about people
(or organizations) in various roles, such as the domain holder or a technician
responsible for domain's name servers.
(:doc:`More about the roles of contacts in the Registry. </Concepts/Contacts>`)

A contact is registered using the command ``create_contact`` (:ref:`display help <epp-client-help>`)
/ ``contact:create`` (:doc:`see the reference </EPPReference/CommandStructure/Create/CreateContact>`)
and required parameters.

.. Note::
   Setting **contact** disclosure preference (disclose flags) requires special attention
   as described in :doc:`/EPPReference/PoliciesRules`.

If you omit:

* ``auth_info``, the server generates one,
* ``disclose``, the server sets disclose flags to defaults according to the disclosure policy,
* other optional parameters, they are left unset.

.. _epp-client-create-nsset:

Create an nsset :sup:`OPTIONAL`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To have the future domain included in the zone, you need to have some
name servers recorded in the Registry as well. Name servers are recorded using :doc:`nsset objects
</EPPReference/ManagedObjects/Nssets>`.

A nsset is registered using the command ``create_nsset`` (:ref:`display help <epp-client-help>`)
/ ``nsset:create`` (:doc:`see the reference </EPPReference/CommandStructure/Create/CreateNsset>`)
and required parameters.

If you omit:

* ``auth_info``, the server generates one,
* ``reportlevel``, the server sets it to the default (see also :doc:`/Concepts/Teccheck`),
* other optional parameters, they are left unset.

.. _epp-client-create-keyset:

Create a keyset :sup:`OPTIONAL`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To have the future domain secured, you need to have some DNSSEC keys recorded in the Registry as well.
The DNSSEC keys are recorded using :doc:`keyset objects
</EPPReference/ManagedObjects/Keysets>`.

A keyset is registered using the command ``create_keyset`` (:ref:`display help <epp-client-help>`)
/ ``keyset:create`` (:doc:`see the reference </EPPReference/CommandStructure/Create/CreateKeyset>`)
and required parameters.

If you omit:

* ``auth_info``, the server generates one,
* ``dnskey``, it will be left empty and the linked domains still will not be secured.

.. _epp-client-create-domain:

Create a domain
^^^^^^^^^^^^^^^

Now, you're ready to actually register a domain name. Domain names are recorded using
:doc:`domain objects </EPPReference/ManagedObjects/Domains>`.

A domain is registered using the command ``create_domain`` (:ref:`display help <epp-client-help>`)
/ ``domain:create`` (:doc:`see the reference </EPPReference/CommandStructure/Create/CreateDomain>`)
and required parameters.

If you omit:

* ``period``, the server makes registration for the smallest period allowed,
* ``auth_info``, the server generates one,
* other optional parameters, they are left unset.

.. rubric:: Conditions for success

* You must be granted access to the zone, in which you want to register the domain.
* You must have credit, if the registry charges for domain creation.

.. _epp-client-reuse:

Re-use
^^^^^^

Of course, if you have previously recorded some contacts, nssets, or keysets,
you may re-use them to register new domains, nssets, and keysets.

Beware, though, other registrars may link your objects to their objects, too.
(This can happen when an object has been transferred.)

.. _epp-client-listing:

Listing objects
---------------

Recorded objects can be retrieved in the form of lists.
This is done in two (or more) steps within separate requests.

The first request asks the server to prepare a list on its side.
Use one of the commands starting with ``prep_*``  (:ref:`display help <epp-client-help>`) /
a listing element (:doc:`see the reference </EPPReference/CommandStructure/List/Prepare>`).

.. Note::
   The list preparation commands that do not accept parameters
   (such as :code:`prep_domains` / :code:`fred:listDomains`),
   will list only objects that you are :term:`designated <designated registrar>`
   to manage.
   The parametrized commands (such as :code:`prep_domains_by_contact` /
   :code:`fred:domainsByContact`) ignore who the designated registrar is.

The server responds with a total of prepared items.

A subsequent request orders the server to send a bulk of list items and it is
to be called repeatedly until the server returns an empty list.

To retrieve the next bulk, use the command ``get_results`` (:ref:`display help <epp-client-help>`)
/ ``fred:getResults`` (:doc:`see the reference </EPPReference/CommandStructure/List/GetResults>`)
which does not require any parameters.

The server retains the remaining list items between these calls.
Another prepare request resets the list.

.. rubric:: Conditions for success

* You must be :ref:`logged in <epp-client-login>`.

.. _epp-client-info:

Getting object information
--------------------------

To view object details, use an ``info`` command according to the object type:

* ``info_domain`` (:ref:`display help <epp-client-help>`)
  / ``domain:info`` (:doc:`see the reference </EPPReference/CommandStructure/Info/InfoDomain>`),
* ``info_contact`` (:ref:`display help <epp-client-help>`)
  / ``contact:info`` (:doc:`see the reference </EPPReference/CommandStructure/Info/InfoContact>`),
* ``info_nsset`` (:ref:`display help <epp-client-help>`)
  / ``nsset:info`` (:doc:`see the reference </EPPReference/CommandStructure/Info/InfoNsset>`),
* ``info_keyset`` (:ref:`display help <epp-client-help>`)
  / ``keyset:info`` (:doc:`see the reference </EPPReference/CommandStructure/Info/InfoKeyset>`).

.. rubric:: Conditions for success

* You must be :ref:`logged in <epp-client-login>`.
* The object must exist.

.. _epp-client-renew:

Renewing domains
----------------

To renew a domain, use the command ``renew_domain`` (:ref:`display help <epp-client-help>`)
/ ``domain:renew`` (:doc:`see the reference </EPPReference/CommandStructure/RenewDomain>`)
and required parameters.

If you don't know its current *expiration date*, you can find out from the domain's
details -- see `Getting object information`_.

If you omit ``period``, the server makes renewal for the smallest period allowed.

.. rubric:: Conditions for success

* You must be :ref:`logged in <epp-client-login>`.
* The domain must exist.
* The domain must not be marked for deletion (\ ``deleteCandidate`` status flag).
* The domain must not be administratively blocked.
* The domain must not be prohibited renewal.
* You must have credit, if the registry charges for domain renewal.

.. _epp-client-transfer:

Transferring objects
--------------------

See the :doc:`/Concepts/Transfer` concept for an explanation of how transfer works in general.

To proceed with a transfer request
(and thus become the :term:`designated registrar` of the object),
use a ``transfer`` command according to the object type:

* ``transfer_domain`` (:ref:`display help <epp-client-help>`)
  / ``domain:transfer`` (:doc:`see the reference </EPPReference/CommandStructure/Transfer/TransferDomain>`),
* ``transfer_contact`` (:ref:`display help <epp-client-help>`)
  / ``contact:transfer`` (:doc:`see the reference </EPPReference/CommandStructure/Transfer/TransferContact>`),
* ``transfer_nsset`` (:ref:`display help <epp-client-help>`)
  / ``nsset:transfer`` (:doc:`see the reference </EPPReference/CommandStructure/Transfer/TransferNsset>`),
* ``transfer_keyset`` (:ref:`display help <epp-client-help>`)
  / ``keyset:transfer`` (:doc:`see the reference </EPPReference/CommandStructure/Transfer/TransferKeyset>`).

.. rubric:: Conditions for success

* You must be :ref:`logged in <epp-client-login>`.
* The object must exist.
* The authinfo must match.
* The object must not be administratively blocked.
* The object must not be prohibited transfers.

.. _epp-client-update:

Updating objects
----------------

Generally, there are 3 "methods" for editing object details:
\ ``add``, ``rem`` (remove), and ``chg`` (change).

\ ``add`` and ``rem`` are used for editing attributes that can have multiple-child values,
such as admin/tech contacts, name servers, or DNS keys. There is no difference
between an omitted child (\ ``NULL``) and a child that contains an empty string (\ ``''``),
both are interpreted as no change.

\ ``chg`` is used to edit single-child values, such as a domain owner, linked nsset,
disclosure preference, or authinfo. If the child is omitted (\ ``NULL``), it means
that a change is not being requested, whereas when a child contains an empty
string (\ ``''``), it means that the old value shall be overwritten
and thus left empty after the update.

To edit object details, use an ``update`` command according to the object type:

* ``update_domain`` (:ref:`display help <epp-client-help>`)
  / ``domain:update`` (:doc:`see the reference </EPPReference/CommandStructure/Update/UpdateDomain>`),
* ``update_contact`` (:ref:`display help <epp-client-help>`)
  / ``contact:update`` (:doc:`see the reference </EPPReference/CommandStructure/Update/UpdateContact>`),
* ``update_nsset`` (:ref:`display help <epp-client-help>`)
  / ``nsset:update`` (:doc:`see the reference </EPPReference/CommandStructure/Update/UpdateNsset>`),
* ``update_keyset`` (:ref:`display help <epp-client-help>`)
  / ``keyset:update`` (:doc:`see the reference </EPPReference/CommandStructure/Update/UpdateKeyset>`).

.. Note::
   Editing **contact** disclosure preference (disclose flags) requires special attention
   as described in :doc:`/EPPReference/PoliciesRules`.

.. rubric:: Conditions for success

* You must be :ref:`logged in <epp-client-login>`.
* The object must exist.
* You must be :term:`designated <designated registrar>` to manage the object.
* The object must not be administratively blocked.
* The object must not be prohibited updates.

.. _epp-client-delete:

Deleting objects
----------------

To delete an object, use a ``delete`` command according to the object type:

* ``delete_domain`` (:ref:`display help <epp-client-help>`)
  / ``domain:delete`` (:doc:`see the reference </EPPReference/CommandStructure/Delete/DeleteDomain>`),
* ``delete_contact`` (:ref:`display help <epp-client-help>`)
  / ``contact:delete`` (:doc:`see the reference </EPPReference/CommandStructure/Delete/DeleteContact>`),
* ``delete_nsset`` (:ref:`display help <epp-client-help>`)
  / ``nsset:delete`` (:doc:`see the reference </EPPReference/CommandStructure/Delete/DeleteNsset>`),
* ``delete_keyset`` (:ref:`display help <epp-client-help>`)
  / ``keyset:delete`` (:doc:`see the reference </EPPReference/CommandStructure/Delete/DeleteKeyset>`).

.. rubric:: Conditions for success

* You must be :ref:`logged in <epp-client-login>`.
* The object must exist.
* You must be :term:`designated <designated registrar>` to manage the object.
* The object must not be linked to (referenced by) other objects.
* The object must not be administratively blocked.
* The object must not be prohibited deletion.

.. _epp-client-polling:

Reading messages
----------------

The server generates service messages.
Reading of the messages is done in two (or more) steps within separate requests.

To ask the server if it has any messages,
use the command ``poll req``  (:ref:`display help <epp-client-help>`)
/ ``<poll op="req"/>`` (:doc:`see the reference </EPPReference/CommandStructure/Poll/PollReq>`).

The server responds with the first message in the queue and the count of messages.

A subsequent request acknowledges that the message has been read and
orders the server to remove it from the queue.

To acknowledge, use the command ``poll ack`` (:ref:`display help <epp-client-help>`)
/ ``<poll op="ack"/>`` (:doc:`see the reference </EPPReference/CommandStructure/Poll/PollAck>`)
with the message identifier.

To read the next message(s), just repeat the process.

If you want to request and acknowledge a message at once in the fred-client,
you may use ``poll_autoack on`` to enable this feature. With autoack on,
the client will send poll request and then automatically poll acknowledge
the read message.

You must be :ref:`logged in <epp-client-login>` to read your messages.

.. _epp-client-credit:

Reading credit
--------------

Just use the command ``credit_info`` (:ref:`display help <epp-client-help>`)
/ ``fred:creditInfo`` (:doc:`see the reference </EPPReference/CommandStructure/CreditInfo>`),
which does not require any parameters.

You must be :ref:`logged in <epp-client-login>`.

.. _epp-client-logout:

Ending a session (logout)
-------------------------

Just use the ``logout`` command (:ref:`display help <epp-client-help>`
/ :doc:`see the reference </EPPReference/CommandStructure/Logout>`),
which does not require any parameters.

Then your client may close the connection (it times out anyway).

If you want to logout, disconnect and quit the fred-client at once, you may use ``quit``.

.. _epp-client-extras:

Additional FRED-client abilities
--------------------------------

This section describes additional abilities of the CLI client.
All these abilities can be used from the running client.

.. Note::
   This guide doesn't describe all features, only highlights. For all fred-client
   features, see the documentation contained with the program.

.. _epp-client-help:

Display command help
^^^^^^^^^^^^^^^^^^^^

To show available fred-client commands, type ``help``.

To show help for a specific command, type :code:`help <command>`
(e.g. :code:`help update_contact`) or :code:`? <command>`
(e.g. :code:`? create_domain`).

.. _epp-client-named-params:

Use named parameters
^^^^^^^^^^^^^^^^^^^^

Command parameters can also be entered by their names, so that you don't have
to watch their order and you don't have to spell out all NULLs and empty lists.

For example, let's say you want to change the notify email of a contact.
Using positional parameters, you would have to enter:

.. code-block:: shell

   > update_contact CID01 (() NULL NULL NULL NULL () NULL () notify@joe.name)

With named parameters, you can enter just this instead:

.. code-block:: shell

   > update_contact CID01 --chg.notify_email=notify@joe.name

Use command help to find out how the composite parameters are structured, e.g.:

.. code-block:: shell

   REG-FRED_A@epp.nic.cz> help update_nsset
   ...

   OPTIONS:
     id (required)            NSSET ID
     add                      Add values
       dns                    List of DNS (list with max 9 items)
         name (required)      Name server
         addr                 Server address (unbounded list)
       tech                   Technical contact ID (unbounded list)
     rem                      Remove values
       name                   Name server (list with max 9 items)
       tech                   Technical contact ID (unbounded list)
     auth_info                Password required by server to authorize the transfer
     reportlevel              Report range level (0 - 10; higher = more detailed)
     cltrid                   Client transaction ID
   ...

If the parameter is indented, you must chain it with parent structures using dots, e.g.
to add a DNS host name, you will need ``--add.dns.name``:

.. code-block:: shell

   > update_nsset ID01 --add.dns.name=ns2.domain.cz --add.dns.addr=217.31.207.130 --rem.name=(ns.2domain.cz)

.. Tip:: Recommended for small modifications of one or two object attributes
   which would have to be entered at the end of a long parameter list.

.. _epp-client-interactive:

Use interactive mode
^^^^^^^^^^^^^^^^^^^^

The interactive mode can be used as a "composer" for complex commands.

To enter parameters of a command interactively, prefix the command with an exclamation
mark :code:`! <command>` (e.g. :code:`! update_contact`) and don't append any parameters yet.
After you press :kbd:`Enter`, you are prompted for the first paramater, then for the second, and so on.

.. code-block:: shell
   :caption: Example

   REG-FRED_A@epp.nic.cz> !update_domain
   Interactive input mode started. Press Ctrl+C to abort or Ctrl+D to finish command.
   Domain name [required]: mydomain.cz
   Add administrative contact ID[1/oo] [optional]: CID02
   Add administrative contact ID[2/oo] [optional]:
   Remove administrative contact ID[1/oo] [optional]:
   Remove temporary contact ID[1/oo] [optional]:
   Change values / NSSET ID [optional]: NID-SET
   Change values / KEYSET ID [optional]:
   Change values / Registrant ID [optional]:
   Change values / Password required by server to authorize the transfer [optional]:
   Validation expires at [optional]:
   Include ENUM domain into ENUM dictionary (y,n) [optional]:
   Client transaction ID [optional]:

   Interactive input completed. [Press Enter]

.. Tip:: Recommended for big or complicated object modifications.

Confirm commands before sending
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before a command is sent to the server, the CLI client may request a special confirmation,
just to give you one more chance to double-check that you're really requesting what you mean.

When enabled, the CLI client will prompt for confirmation as follows:

.. code-block:: shell

   Command to issue:
   update_domain mydomain.cz CID02 () () (NID-SET)
   Do you really want to send this command to the server? (y/N): y

To enable confirmation, type ``confirm on``. To disable it, type ``confirm off``.

View raw EPP messages
^^^^^^^^^^^^^^^^^^^^^

The CLI client allows you to read the XML-formatted communication. You can either
increase the verbosity to level 3 with :code:`verbose 3` and then you will see
the XML messages for requests and replies each time.

Or if you need to see the XML only occasionally, you may use ``raw-command``
to display the last composed request, or ``raw-answer`` to display the last
received reply.
