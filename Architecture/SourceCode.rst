
.. _FRED-Arch-Source:

Source code
===========

Source code is divided into several subprojects.

The subprojects belong to one of the following groups depending on which tools
are used to build/install them:

* "A" stands for autotools (used with C++ code),
* "D" stands for FRED distutils (used with Python code).

Each subproject has its own GitHub repository.

.. rubric:: List of the subprojects and repositories

* :ref:`A <install-auto>` `fred-akm <https://www.github.com/CZ-NIC/fred-akm.git>`_
  – a CLI CORBA client for automatic keyset management
* :ref:`A <install-auto>` `fred-cdnskey-scanner <https://www.github.com/CZ-NIC/fred-cdnskey-scanner.git>`_
  – a CLI tool to scan a set of domains for CDNSKEY records
* :ref:`D <install-dist>` `fred-client <https://www.github.com/CZ-NIC/fred-client.git>`_
  – a Python EPP client – a CLI application and an API library
* :ref:`A <install-auto>` `fred-db <https://www.github.com/CZ-NIC/fred-db.git>`_
  – a collection of SQL scripts to set up the database in PostgreSQL
* :ref:`D <install-dist>` `fred-doc2pdf <https://www.github.com/CZ-NIC/fred-doc2pdf.git>`_
  – a Python wrapper over ``rml2pdf`` used for generation of some PDF documents
* :ref:`A <install-auto>` `fred-idl <https://www.github.com/CZ-NIC/fred-idl.git>`_
  – IDL interface definitions for CORBA inter-process communication
* :ref:`A <install-auto>` `fred-mod-corba <https://www.github.com/CZ-NIC/fred-mod-corba.git>`_
  – an Apache module serving other two modules (EPP, WHOIS) the common functionality of CORBA communication
* :ref:`A <install-auto>` `fred-mod-eppd <https://www.github.com/CZ-NIC/fred-mod-eppd.git>`_
  – an Apache module for parsing EPP commands and transforming them into CORBA calls to a back-end server (and vice versa)
* :ref:`A <install-auto>` `fred-mod-whoisd <https://www.github.com/CZ-NIC/fred-mod-whoisd.git>`_
  – an Apache module for processing WHOIS commands and transforming them into CORBA calls to a back-end server (and vice versa)
* :ref:`D <install-dist>` `fred-pyfred <https://www.github.com/CZ-NIC/fred-pyfred.git>`_
  – a Python CORBA server and clients for zone-file generation, email communication, technical checks and file-manager components
* :ref:`D <install-dist>` `fred-rdap <https://www.github.com/CZ-NIC/fred-rdap.git>`_
  – an RDAP server (front end) prototype implemented with Django
* :ref:`A <install-auto>` `fred-server <https://www.github.com/CZ-NIC/fred-server.git>`_
  – C++ CORBA servers (back end) for the core registry functionality and a CLI administration tool
* :ref:`D <install-dist>` `fred-transproc <https://www.github.com/CZ-NIC/fred-transproc.git>`_
  – a Python script for querying various sources of bank transactions and processing them with FRED (tied to Czech environment)
* :ref:`D <install-dist>` `fred-webadmin <https://www.github.com/CZ-NIC/fred-webadmin.git>`_
  – the Daphne web administration server (front end) for registry customer support (mainly registrar creation and activity inspection)
* :ref:`D <install-dist>` `fred-webwhois <https://www.github.com/CZ-NIC/fred-webwhois.git>`_
  – the web WHOIS server (front end) implemented with Django

* :ref:`D <install-dist>` `fred-utils-distutils <https://www.github.com/CZ-NIC/fred-utils-distutils.git>`_
  – a Python wrapper over ``python-setuptools`` (necessary for installation of some FRED subprojects in Python)
* :ref:`D <install-dist>` `fred-utils-pyfco <https://www.github.com/CZ-NIC/fred-utils-pyfco.git>`_
  – a Python wrapper over CORBA
* :ref:`D <install-dist>` `fred-utils-pylogger <https://www.github.com/CZ-NIC/fred-utils-pylogger.git>`_
  – a Python wrapper over logging infrastructure for all Python clients
