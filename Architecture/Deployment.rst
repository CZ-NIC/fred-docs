


Distributed deployment example
-------------------------------

Deploying FRED on multiple servers brings at least two advantages:

* increased performance,
* access control on the network level.

Deploying on multiple physical servers is not the only distributed solution,
deploying on virtual servers or separating tasks on the process level is also
possible.

.. rubric:: Nodes overview

Nodes in this document represent execution environments.

We work with the following nodes:

* `EPP node`_ -- EPP service
* `ADMIN node`_ -- web admin service
* `WEB node`_ -- public web services: WHOISes, RDAP, Domain Browser [#ext]_
* `HM node`_ -- zone management
* `APP node`_ -- application servers, CLI admin tools, pgbouncer, CORBA naming
  service
* :ref:`DB node <deploy-db>` -- the main FRED database
* :ref:`LOGDB node <deploy-db>` -- the logger database
* MOJEID node [#ext]_ -- MojeID service, web and database

.. [#ext] MojeID and Domain Browser are :term:`CZ-specific` :doc:`extensions
   </Features/Extensions>`, and they are not described further.

.. _hw-params-note:

.. Note::

   .. rubric:: Hardware parameters background

   The hardware parameters described further are minimum requirements
   for a Registry of about 1 million domains and with this approximate traffic:

   * EPP:
      * write operations: ~ 3,5 million / month (they increase the size of both :ref:`databases <deploy-db>`)
      * read-only operations: ~ 30 million / month (they increase the size of ``logdb``)
   * **WHOIS:** 15 million operations / month (they increase the size of ``logdb``)

   WHOIS includes both Unix and Web variant, and RDAP, too.

.. Tip::

   .. rubric:: Redundancy

   This text does not describe redundancy options in detail, but here is a quick tip:

   * database replication is a standard technique to protect data,
   * the whole system can be replicated in several instances on different
     localities, which can substitute one another when one instance fails or
     during a system upgrade.

.. contents::
   :local:
   :backlinks: none

.. _deploy-network:

Network
^^^^^^^^

Network rules are described further per node, but here is an overview of logical
connections in the network (one instance).

.. _fig-deployment-network:

.. figure:: /Architecture/_graphics/schema-network.png
   :alt:
   :align: center
   :figwidth: 100%

   Network -- Logical topology

.. _deploy-ports:

.. Note::

   .. rubric:: Ports

   The port numbers mentioned in the network rules are settings
   of the default installation.

.. _deploy-epp:

EPP node
^^^^^^^^^^^

Services: EPP service

Packages:

* libapache2-mod-corba
* libapache2-mod-eppd

Hardware parameters (:ref:`see the background <hw-params-note>`):

* CPU: @2.0 GHz, 10 cores
* Memory: 16 GB--32 GB
* Storage: 200 GB

Network:

* access to EPP (tcp, port 700) permitted only from particular IP addresses
  (or ranges) declared by registrars

.. list-table:: Network rules for CORBA clients on the EPP node
   :widths: 10 20 2 5 5 10 20
   :header-rows: 1

   * - Service
     - Description
     -
     - Server
     - Protocol /Port
     - Service
     - Description
   * - apache2 |br| mod-eppd
     - registrar interface/epp service
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2224 <deploy-ports>`
     - fred-rifd
     - FRED registrar interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon

.. _deploy-admin:

ADMIN node
^^^^^^^^^^^

Services: WebAdmin service

Packages:

* fred-common
* fred-idl
* fred-pyfco
* fred-pylogger
* fred-webadmin

Hardware parameters (:ref:`see the background <hw-params-note>`):

* CPU: @2.0 GHz, 10 cores
* Memory: 16 GB--32 GB
* Storage: 200 GB

Network:

* access to HTTPS (tcp, port 443) permitted only from the private network of
  the Registry

.. list-table:: Network rules for CORBA clients on the ADMIN node
   :widths: 10 20 2 5 5 10 20
   :header-rows: 1

   * - Service
     - Description
     -
     - Server
     - Protocol /Port
     - Service
     - Description
   * - webadmin/daphne
     - web based registry administration
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2222 <deploy-ports>`
     - fred-adifd
     - FRED administration interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2228 <deploy-ports>`
     - fred-msgd
     - FRED messaging daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2234 <deploy-ports>`
     - fred-rsifd
     - FRED registry record statement daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2232 <deploy-ports>`
     - fred-pyfred\@filemanager
     - FRED pyfred service -- filemanager module


.. _deploy-web:

WEB node
^^^^^^^^^^^

Services: Unix WHOIS, Web WHOIS, RDAP

Packages:

* fred-idl
* fred-pyfco
* fred-pylogger
* fred-rdap
* fred-webwhois
* libapache2-mod-corba
* libapache2-mod-whoisd

Hardware parameters (:ref:`see the background <hw-params-note>`):

* CPU: @2.0 GHz, 10 cores
* Memory: 16 GB--32 GB
* Storage: 200 GB

Network:

* access to HTTPS (tcp, port 443) permitted from anyone
* access to WHOIS (tcp, port 43) permitted from anyone

.. list-table:: Network rules for CORBA clients on the WEB node
   :widths: 10 20 2 5 5 10 20
   :header-rows: 1

   * - Service
     - Description
     -
     - Server
     - Protocol /Port
     - Service
     - Description
   * - apache2 |br| mod-whoisd
     - unix whois service (rfc 3912)
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2223 <deploy-ports>`
     - fred-pifd
     - FRED public interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon
   * - nginx
     - web whois service
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2223 <deploy-ports>`
     - fred-pifd
     - FRED public interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2234 <deploy-ports>`
     - fred-rsifd
     - FRED registry record statement daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon
   * - nginx
     - rdap service
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2223 <deploy-ports>`
     - fred-pifd
     - FRED public interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon


.. _deploy-hm:

HM node
^^^^^^^^^^

Hidden master for the DNS infrastructure.

Services: zone file generation, zone signing, notifying DNS servers

Packages:

* fred-idl
* pyfred-genzone
* python-pyfred

Hardware parameters (:ref:`see the background <hw-params-note>`):

* CPU: @2.0 GHz, 10 cores
* Memory: 16 GB--32 GB
* Storage: 200 GB

Network:

* access to IXFR (tcp, port 53) permitted only from DNS servers

.. list-table:: Network rules for CORBA clients on the HM node
   :widths: 10 20 2 5 5 10 20
   :header-rows: 1

   * - Service
     - Description
     -
     - Server
     - Protocol /Port
     - Service
     - Description
   * - genzone-client
     - zone file generator
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2231 <deploy-ports>`
     - fred-pyfred\@genzone
     - FRED pyfred service -- genzone module

.. _deploy-app:

APP node
^^^^^^^^^^^

Services:

* CORBA naming service (omninames) as a virtual server "corba",
* backend application servers,
* CLI administration tools,
* :program:`pgbouncer` -- prepares and recycles database connections to decrease
  overhead costs

Packages:

* cdnskey-scanner
* fred-akm
* fred-common
* fred-doc2pdf
* fred-idl
* fred-logger-maintenance
* fred-server: fred-adifd, fred-akmd, fred-logd, fred-pifd, fred-rifd,
  fred-rsifd
* fred-transproc
* python-pyfred, fred-pyfred, pyfred-filemanager

.. fred-dbifd, fred-mifd, fred-msgd

Hardware parameters (:ref:`see the background <hw-params-note>`):

* CPU: @2.0 GHz, 10 cores
* Memory: 16 GB--32 GB
* Storage: 400 GB

  .. Note:: Consider that the storage will contain files managed by the FRED
     File Manager.

Network:

* only internal access from the private network of the Registry

.. list-table:: Network rules for CORBA clients on the APP node
   :widths: 10 20 2 5 5 10 20
   :header-rows: 1

   * - Service
     - Description
     -
     - Server
     - Protocol /Port
     - Service
     - Description
   * - fred-akm
     - fred-akm
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2233 <deploy-ports>`
     - fred-akmd
     - FRED AKM interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service - mailer module
   * - fred-admin
     - fred-admin
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2224 <deploy-ports>`
     - fred-rifd
     - FRED registrar interface daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2232 <deploy-ports>`
     - fred-pyfred\@filemanager
     - FRED pyfred service -- filemanager module
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module



.. list-table:: Network rules for CORBA servers on the APP node
   :widths: 10 20 2 5 5 10 20
   :header-rows: 1

   * - Service
     - Description
     -
     - Server
     - Protocol /Port
     - Service
     - Description
   * - fred-logd
     - FRED logging daemon
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * - fred-rifd
     - FRED registrar interface daemon
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2229 <deploy-ports>`
     - fred-pyfred\@techcheck
     - FRED pyfred service -- techcheck module
   * - fred-akmd
     - FRED AKM interface daemon
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon daemon
   * - fred-adifd
     - FRED administration interface daemon
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module
   * - fred-msgd
     - FRED messaging daemon
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2232 <deploy-ports>`
     - fred-pyfred\@filemanager
     - FRED pyfred service -- filemanager module
   * - fred-pifd
     - FRED public interface daemon
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2226 <deploy-ports>`
     - fred-logd
     - FRED logging daemon daemon
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2232 <deploy-ports>`
     - fred-pyfred\@filemanager
     - FRED pyfred service -- filemanager module
   * - fred-rsifd
     - FRED
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2232 <deploy-ports>`
     - fred-pyfred\@filemanager
     - FRED pyfred service -- filemanager module
   * - fred-pyfred\@genzone
     - FRED pyfred service -- genzone module
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2232 <deploy-ports>`
     - fred-pyfred\@filemanager
     - FRED pyfred service -- filemanager module
   * - fred-pyfred\@filemanager
     -  FRED pyfred service -- filemanager module
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer):
     - connection pooler for PostgreSQL
   * - fred-pyfred\@techcheck
     - FRED pyfred service -- techcheck module
     - →
     - localhost
     - tcp/:ref:`5432 <deploy-ports>`
     - pgbouncer
     - connection pooler for PostgreSQL
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2809 <deploy-ports>`
     - omninames
     - OmniORB Interoperable Naming Service
   * -
     -
     - →
     - :ref:`corba <deploy-app>`
     - tcp/:ref:`2225 <deploy-ports>`
     - fred-pyfred\@mailer
     - FRED pyfred service -- mailer module

.. _deploy-db:

Database nodes
^^^^^^^^^^^^^^^^^

Database is separated into two nodes:

* DB -- the main database ``freddb`` -- data of all domains, contacts, registrars, history etc.
* LOGDB -- the :doc:`audit log (logger) </Concepts/AuditLog>` database ``logdb`` -- logging of all
  user transactions

We have the logger database separately due to high workload.

Packages:

* fred-db

Hardware parameters (:ref:`see the background <hw-params-note>`) -- DB:

* CPU: 2x @2.0 GHz, at least 10 cores per CPU
* Memory: 32 GB--64 GB

  .. Note:: Consider that,
     ideally, this whole database should fit into the memory,
     which is possible only till a certain number of objects though.
     See also *Storage* considerations.

* Storage: 400 GB

  .. Note:: Consider:

     * storage size can be even smaller depending on the size of the database,
       which depends on the number of objects in the :term:`db` and registrars'
       behaviour (growth of object history),
     * the size of the database after 5-year operation of a registry of 1 million
       domains can be about 30 GB,
     * extra space for garbage accumulation (before vacuuming),
       temporary dumps during migrations, and other :term:`db` maintenance costs.

Hardware parameters (:ref:`see the background <hw-params-note>`) -- LOGDB:

* CPU: 2x @2.0 GHz, at least 10 cores per CPU
* Memory: 32 GB--64 GB

  .. Note:: Consider this the lowest requirement.
     This amount of memory might be filled quite soon.

* Storage

  .. Note:: Consider:

     * how many months of logs are necessary to be kept in the database
       (the last year? the two last years?) and how much logs can be kept
       in backups,
     * growth rate of the log records (according to the traffic estimation
       as described :ref:`above <hw-params-note>`):
       EPP ~ 135 GB / month, WHOIS ~ 30 GB / month.

Network:

* accessed only by the backend server(s) from the :ref:`APP node <deploy-app>`

.. _deploy-diagram:

Component deployment diagram
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _fig-deployment:

.. figure:: /Architecture/_graphics/schema-deployment.png
   :alt:
   :align: center
   :figwidth: 100%

   Diagram of FRED components deployed on multiple nodes
