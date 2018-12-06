
.. _FRED-Arch-clients:

CORBA clients
-------------

The CORBA clients constitute the frontend interfaces that serve actual users.

.. contents::
   :local:
   :backlinks: none



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
script), transforms it into an internal XML format
and calls :ref:`pain <FRED-Arch-clients-pain>` to save this data into the
**PAIN** database.

The script has its own configuration file.

See also :doc:`/Concepts/PAIN`.

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
keyset management </Concepts/AKM>` and is used to perform
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

Neither a configuration file nor database access are required.
The scanner reads from STDIN and writes to STDOUT.

.. _FRED-Arch-clients-pain:

PAIN utility & admin service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This utility collects and parses payments, and saves them to an independent
database. It is based on `Django <https://www.djangoproject.com/>`_.

The utility allows to pair processed payments with a registrar
credit account and invoices in FRED, either automatically or manually using
the Django admin interface.

The ``fred-pain`` module connects this independent utility to FRED over CORBA.

See also :doc:`/Concepts/PAIN`.



Public interface
^^^^^^^^^^^^^^^^

This interface provides information services to the public.

.. _FRED-Arch-clients-unixwhois:

Unix whois service
~~~~~~~~~~~~~~~~~~

This service implements the WHOIS protocol as described in :rfc:`3912`.
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

It is based on `Django <https://www.djangoproject.com/>`_.

.. _FRED-Arch-clients-rdap:

RDAP service
~~~~~~~~~~~~

This service processes queries sent via the HTTP protocol using the REST API.
If the query is successful, the response contains JSON-formatted data.

It is based on `Django <https://www.djangoproject.com/>`_.
