
.. _FRED-Arch-servers:

CORBA servers
-------------
This is a set of components which implement the backend of the Registry and
which can run independently of each other.
All of them use the same ORB implementation
(`omniORB <http://omniorb.sourceforge.net>`_) which takes care
of the server side and process threading.

.. _FRED-Arch-servers-cpp:

C++ daemons
^^^^^^^^^^^
These backend components are coded in C++.

Each of them is launched in a separate process and they may share
a single :ref:`configuration <config-servers-cpp>` file.

.. _FRED-Arch-servers-rif:

fred-rifd
~~~~~~~~~
The registrar interface :ref:`daemon <FRED-Arch-servers-cpp>`.

This daemon implements operations over the database defined in the EPP protocol
and it is used by the :ref:`EPP service <FRED-Arch-clients-epp>`.
Every EPP operation is mapped to a corresponding CORBA operation.
Operations over objects are *idempotent*, i.e. if the same operation is invoked
repeatedly, it does not change the state of object in the Registry.

The daemon is aware of all connected clients; if a client connects
in a new session, a unique identifier is generated to identify the session
in EPP communication and in the audit log.

All clients' activity is recorded in the database including the original
request and response XML files.

Object-altering operations make the system record the object in the history
before the change is applied.

A database connection is opened during each EPP operation (and closed
at the end). Therefore the :program:`pgpool` tool is utilized to cache
the connections, thus reducing the connection overhead.

.. _FRED-Arch-servers-pif:

fred-pifd
~~~~~~~~~
The public interface :ref:`daemon <FRED-Arch-servers-cpp>`.

This daemon implements operations over the database which make information
about domains accessible to the public; it functions as the backend for
the :ref:`unix whois <FRED-Arch-clients-unixwhois>`,
:ref:`web whois <FRED-Arch-clients-webwhois>` and
:ref:`RDAP <FRED-Arch-clients-rdap>`.

.. _FRED-Arch-servers-rsif:

fred-rsifd
~~~~~~~~~~
The record statement interface :ref:`daemon <FRED-Arch-servers-cpp>`.

This daemon implements operations over the database which allow generation
of signed PDF documents with information about registrable objects;
it functions as another backend for
:ref:`Daphne <FRED-Arch-clients-webadmin>`,
:ref:`web whois <FRED-Arch-clients-webwhois>` and
Domain Browser extension.

.. _FRED-Arch-servers-adif:

fred-adifd
~~~~~~~~~~
The administration interface :ref:`daemon <FRED-Arch-servers-cpp>`.

This daemon implements administration operations over the database which allow
to browse any information in the Registry (including the history and audit log)
and to add and modify some of it.

It functions as the backend for Daphne, the :ref:`web administration service
<FRED-Arch-clients-webadmin>`.

.. _FRED-Arch-servers-akmd:

fred-akmd
~~~~~~~~~
The automatic keyset management :ref:`daemon <FRED-Arch-servers-cpp>`.

This daemon implements operations over the database that support automatic
management of keysets (loading domains with name servers, updating DNSSEC,
notifying contacts); it functions as the backend for the :ref:`AKM client
<FRED-Arch-clients-akm>`.

.. _FRED-Arch-servers-msg:

fred-msgd
~~~~~~~~~
The messaging :ref:`daemon <FRED-Arch-servers-cpp>`.

This daemon implements operations for generating and sending text messages (SMS)
and printed letters.

.. _FRED-Arch-servers-log:

fred-logd
~~~~~~~~~
The audit logging :ref:`daemon <FRED-Arch-servers-cpp>` or "logger".

This daemon creates audit trail of all user activity that passes
through FRED applications and modules (i.e. CORBA clients, see the
:ref:`fig-arch-components`).

.. _FRED-Arch-servers-mif:

fred-mifd
~~~~~~~~~
The :ref:`daemon <FRED-Arch-servers-cpp>` of the MojeID extension.

This daemon implements operations for the :ref:`MojeID extension
<FRED-Features-Extensions>`.

.. _FRED-Arch-servers-dbif:

fred-dbifd
~~~~~~~~~~
The :ref:`daemon <FRED-Arch-servers-cpp>` of the Domain Browser extension.

This daemon implements operations for the :ref:`Domain Browser extension
<FRED-Features-Extensions>`.

.. _FRED-Arch-servers-py:

PYFRED daemon(s)
^^^^^^^^^^^^^^^^
These backend components are coded in Python.

The PYFRED is a framework which provides common functions to several modules
that act as standalone CORBA servers and implement various operations
over the database.

The common functions provided by the framework encompass:

* process logging,
* database connection management,
* parsing of a configuration file,
* ORB initialization and registration of objects with the CORBA naming service,
* launching of periodic tasks registered by the modules.

The modules can run either in a single process or in several processes and
they may share a single :ref:`configuration <config-servers-py>` file.

.. A module in the context of PYFRED is a Python module containing the ``init``
   function which is called when the module is loaded. The initialization function
   returns a CORBA object and the name under which the object is registered
   with the naming service, and the framework takes care of making the module
   accessible from the outside. The module interracts with the framework
   only during initialization and after that, it has a life of its own.

.. _FRED-Arch-servers-genzone:

GenZone
~~~~~~~

The zone generator :ref:`daemon <FRED-Arch-servers-py>`.

This daemon implements operations over the database used during zone file
generation.

A generation is requested by the :ref:`client application
<FRED-Arch-clients-genzone>` that can run on another
machine. The client receives a portion of data of a fixed size, first,
and then orders the remaining data in small chunks. (The total size of a zone
file can reach hundreds of MB.)

.. _FRED-Arch-servers-mailer:

Mailer
~~~~~~

The mailer :ref:`daemon <FRED-Arch-servers-py>`.

This daemon implements the part of the notification system that delivers
messages through email. It integrates a templating system for email
assembly, operations for sending and archivation of outgoing email and search
in archived messages.

.. Note:: The mailer does not send email by itself, it just hands all email over
   to a mail transfer agent.

Attachments are either constructed from templates or retrieved from the file
manager.

The mailer is used by the CORBA servers `fred-rifd`_, `fred-adifd`_, `TechCheck`_,
and also by the CORBA clients :ref:`WebAdmin <FRED-Arch-clients-webadmin>` and
MojeID extension.

.. _FRED-Arch-servers-filemanager:

FileManager
~~~~~~~~~~~

The file manager :ref:`daemon <FRED-Arch-servers-py>`.

This daemon implements operations for managing files, namely the upload,
download and search of managed files.
Each file is stored in the file system as such and only its metadata are
recorded in the database.

The file manager is used by :ref:`mailer <FRED-Arch-servers-mailer>`,
:ref:`web whois service <FRED-Arch-clients-webwhois>` and file manager client.

.. _FRED-Arch-servers-techcheck:

TechCheck
~~~~~~~~~

The technical checks :ref:`daemon <FRED-Arch-servers-py>`.

This daemon implements operations for performing technical tests on name server
sets.

The tests are either launched periodically and a report is sent to the
corresponding technical contact of the nsset by email, or they are requested
by registrars and the reports are included in EPP poll messages.

The technical tests are scaled by severity and the tests of higher
severity can be performed only if the tests of lower severity were successful.

Both planned checks and results are stored in the database.
