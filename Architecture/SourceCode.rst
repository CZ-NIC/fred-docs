
.. _FRED-Arch-Source:

Source code
===========

Source code is divided into several subprojects.

Each subproject has its own GitHub repository.

.. rubric:: List of the subprojects and repositories

* `fred-akm <https://www.github.com/CZ-NIC/fred-akm.git>`_
  – a CLI CORBA client for automatic keyset management
* `fred-cdnskey-scanner <https://www.github.com/CZ-NIC/fred-cdnskey-scanner.git>`_
  – a CLI tool to scan a set of domains for CDNSKEY records
* `fred-client <https://www.github.com/CZ-NIC/fred-client.git>`_
  – a Python EPP client – a CLI application and an API library
* `fred-db <https://www.github.com/CZ-NIC/fred-db.git>`_
  – a collection of SQL scripts to set up the database in PostgreSQL
* `fred-doc2pdf <https://www.github.com/CZ-NIC/fred-doc2pdf.git>`_
  – a Python wrapper over ``rml2pdf`` used for generation of some PDF documents
* `fred-idl <https://www.github.com/CZ-NIC/fred-idl.git>`_
  – IDL interface definitions for CORBA inter-process communication
* `fred-mod-corba <https://www.github.com/CZ-NIC/fred-mod-corba.git>`_
  – an Apache module serving other two modules (EPP, WHOIS) the common functionality of CORBA communication
* `fred-mod-eppd <https://www.github.com/CZ-NIC/fred-mod-eppd.git>`_
  – an Apache module for parsing EPP commands and transforming them into CORBA calls to a back-end server (and vice versa)
* `fred-mod-whoisd <https://www.github.com/CZ-NIC/fred-mod-whoisd.git>`_
  – an Apache module for processing WHOIS commands and transforming them into CORBA calls to a back-end server (and vice versa)
* `fred-pyfred <https://www.github.com/CZ-NIC/fred-pyfred.git>`_
  – a Python CORBA server (back end) and clients for zone-file generation, email communication, technical checks and file-manager components
* `fred-rdap <https://www.github.com/CZ-NIC/fred-rdap.git>`_
  – an RDAP server (front end) prototype implemented with Django
* `fred-server <https://www.github.com/CZ-NIC/fred-server.git>`_
  – C++ CORBA servers (back end) for the core registry functionality and a CLI administration tool
* `fred-transproc <https://www.github.com/CZ-NIC/fred-transproc.git>`_
  – a Python script for querying various sources of bank transactions and processing them with FRED (tied to Czech environment)
* `fred-webadmin <https://www.github.com/CZ-NIC/fred-webadmin.git>`_
  – the Daphne web administration server (front end) for registry customer support (mainly registrar creation and activity inspection)
* `fred-webwhois <https://www.github.com/CZ-NIC/fred-webwhois.git>`_
  – the web WHOIS server (front end) implemented with Django

* `fred-utils-distutils <https://www.github.com/CZ-NIC/fred-utils-distutils.git>`_
  – a Python wrapper over ``python-setuptools`` (necessary for installation of all FRED subprojects in Python)
* `fred-utils-pyfco <https://www.github.com/CZ-NIC/fred-utils-pyfco.git>`_
  – a Python wrapper over CORBA
* `fred-utils-pylogger <https://www.github.com/CZ-NIC/fred-utils-pylogger.git>`_
  – a Python wrapper over logging infrastructure for all Python clients
