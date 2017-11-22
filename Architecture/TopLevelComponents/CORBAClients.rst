
.. _FRED-Arch-clients:

CORBA clients
-------------

The CORBA clients constitute the frontend interfaces that serve actual users.

Registrar interface
^^^^^^^^^^^^^^^^^^^^

This interface provides only a single service to the registrars.

.. _FRED-Arch-clients-epp:

EPP service
~~~~~~~~~~~

This service negotiates communication between registrars and the Registry
by means of the :term:`EPP` protocol which was designed for creation and
administration of registrable objects.

The :program:`mod-eppd` module translates the incoming requests in XML
into remote CORBA calls (supported by the :program:`mod-corba` module)
and then translates their results back to the outgoing responses in XML.
The structure of the XML documents is formally described in XML schemas
and can be validated.

The communication is secured with the SSL using the :program:`mod-ssl`
Apache module. Transportation is provided by the TCP/IP protocols.

The service is built on a web server engine (Apache). It has its own
configuration in the Apache config. syntax.


Administration interface
^^^^^^^^^^^^^^^^^^^^^^^^

This interface provides the web service and command-line utilities
for Registry administration.

.. NOTE Admin tools are not complete (other pyfred clients are missing)

.. _FRED-Arch-clients-webadmin:

WebAdmin service (Daphne)
~~~~~~~~~~~~~~~~~~~~~~~~~

This service provides web access to Registry administration. It can be used
by the Registry customer service for manual administrative tasks.

This component is coded in Python using the CherryPy framework which provides
a self-contained web server.

The service has its own configuration file.

.. _FRED-Arch-clients-genzone:

Genzone client
~~~~~~~~~~~~~~

The genzone client is a command-line application functioning as the client
counterpart of the GenZone server. It is used to request and receive data
to generate the actual zone file.

The client has its own configuration file.

.. _FRED-Arch-clients-transproc:

Transproc
~~~~~~~~~

This Python script is used to download and analyze transcripts
of bank transactions or simple payments. It parses a downloaded transcript,
whose format is specific to each bank, using a *processor* (configurable
script), transforms it into the internal XML format recognized by the FRED
and calls the :program:`fred-admin` to import this data into the database.

The script has its own configuration file.

.. _FRED-Arch-clients-admin:

Fred-admin
~~~~~~~~~~

This command-line application is used mainly (but not only) for automated
administration tasks, such as keeping object states up to date,
cancelling expired domains, deleting unused objects, generating notifications
and billing registrars.
Refer to ``fred-admin --help`` for all available commands.

This program shares configuration with C++ daemons.

.. _FRED-Arch-clients-akm:

Fred-akm
~~~~~~~~~

This command-line application implements the processing logic of :doc:`automatic
keyset management </Features/Concepts/AKM>` and is used to perform
the :ref:`periodic task <cronjob-akm>`.
Refer to ``fred-akm --help`` for all available commands.

The program has its own :ref:`configuration <config-cliutils>` file.

The program uses a local SQLite database to store internal intermediary data
(scan state) between runs.

.. _FRED-Arch-clients-cdnskeyscanner:

CDNSKEY scanner
~~~~~~~~~~~~~~~

This command-line utility is used during automatic management of keysets
to scan specified name servers for requests to update DNSSEC keys
of specified domains. The utility spreads queries over a specified run time
to avoid overloading the DNS infrastructure and distributes queries per
name server.

The utility is implemented with the `getdns <https://getdnsapi.net/>`_ and
`libevent <http://libevent.org/>`_ APIs.

No configuration file nor database access required.
The scanner reads from STDIN and writes to STDOUT.


Public interface
^^^^^^^^^^^^^^^^

This interface provides information services to the public.

.. _FRED-Arch-clients-unixwhois:

Unix whois service
~~~~~~~~~~~~~~~~~~

This service implements the WHOIS protocol as described in `RFC 3912
<https://tools.ietf.org/html/rfc3912>`_.
The protocol allows to query the Registry about registrable objects.

The :program:`mod-whoisd` module translates incoming WHOIS requests
into remote CORBA calls (supported by the :program:`mod-corba` module)
and then translates their results back to outgoing WHOIS responses.

Each response contains the link to the web whois service site which can be used to win full information about domain owners and administrative contacts.

The unix whois service allows to query even ENUM domains, although these
responses do not contain the link to the web whois because the rules
of information disclosure that apply to ENUM domains are different from those
of common domains.

The service is built on a web server engine (Apache). It has its own
configuration in the Apache config. syntax.

.. _FRED-Arch-clients-webwhois:

Web whois service
~~~~~~~~~~~~~~~~~~

This service allows to browse the database of the Registry. It allows to search
in domains, contacts, name server sets and DNS key sets.
The web site is protected against data mining with CAPTCHA.

This service does not allow to browse information about ENUM domains.

The service is built on a web server engine (any).

.. _FRED-Arch-clients-rdap:

RDAP service
~~~~~~~~~~~~

This service processes queries sent via the HTTP protocol using the REST API.
If the query is successful, the response contains JSON-formatted data.

The service is built on a web server engine (any).



Extending services
^^^^^^^^^^^^^^^^^^
Extensions are optional applications which are not a part of the FRED
as such. As standalone applications, they use the FRED daemons (CORBA
servers) to access the FRED database.

.. _FRED-Arch-clients-mid:

MojeID
~~~~~~
This service allows users to log in with a single username and password to any
web service that supports the MojeID authentication, from any computer or
mobile device.

The service is built on a web server engine (any).

.. _FRED-Arch-clients-db:

Domain browser
~~~~~~~~~~~~~~
This service gives an overview of domains, name server sets
and DNS key sets which are linked to the contact of a logged-in user
in the Registry. The user logs in using the MojeID service.

The service is built on a web server engine (any).
