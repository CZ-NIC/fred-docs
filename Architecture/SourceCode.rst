
.. _FRED-Arch-Source:

Source code
===========

The source code of FRED is divided into several subprojects.

The subprojects belong to one of the following groups depending on which tools
are used to build them:

* ::A:: stands for Autotools (used only in :file:`fred-db`),
* ::C:: stands for CMake (used with C++ code),
* ::S:: stands for Python Setuptools.

Each subproject has its own GitHub repository.

Subprojects and repositories
----------------------------

.. rubric:: Core

* :ref:`::C:: <install-cmake>` :repo:`fred-akm`
  – a CLI CORBA client for automated keyset management
* :ref:`::C:: <install-cmake>` :repo:`fred-cdnskey-scanner`
  – a CLI tool to scan a set of domains for CDNSKEY records
* :ref:`::S:: <install-setup>` :repo:`fred-client`
  – a Python EPP client – a CLI application and an API library
* :ref:`::A:: <install-auto>` :repo:`fred-db`
  – a collection of SQL scripts to set up the database in PostgreSQL
* :ref:`::S:: <install-setup>` :repo:`fred-doc2pdf`
  – a Python wrapper over ``rml2pdf`` used for generation of PDF documents
* :ref:`::C:: <install-cmake>` :repo:`fred-idl`
  – IDL interface definitions for CORBA inter-process communication
* :ref:`::C:: <install-cmake>` :repo:`fred-libfred`
  – a C++ library implementing operations on core registry objects (dependency for ``fred-server``)
* :ref:`::C:: <install-cmake>` :repo:`fred-mod-corba`
  – an Apache module serving other two modules (EPP, WHOIS) the common functionality of CORBA communication
* :ref:`::C:: <install-cmake>` :repo:`fred-mod-eppd`
  – an Apache module for parsing EPP commands and transforming them into CORBA calls to a back-end server (and vice versa)
* :ref:`::C:: <install-cmake>` :repo:`fred-mod-whoisd`
  – an Apache module for processing WHOIS commands and transforming them into CORBA calls to a back-end server (and vice versa)
* :ref:`::S:: <install-setup>` :repo:`fred-pyfred`
  – a Python CORBA server and clients for zone-file generation, email communication, and technical checks, including file-manager components
* :ref:`::S:: <install-setup>` :repo:`fred-rdap`
  – an RDAP server (front end) prototype implemented with Django
* :ref:`::C:: <install-cmake>` :repo:`fred-server`
  – C++ CORBA servers (back end) for the core registry functionality and a CLI administration tool
* :ref:`::S:: <install-setup>` :repo:`fred-webadmin`
  – the Daphne web administration server (front end) for registry customer support (mainly registrar creation and activity inspection)
* :ref:`::S:: <install-setup>` :repo:`fred-webwhois`
  – the web WHOIS server (front end) implemented with Django

.. rubric:: Utilities

* :ref:`::S:: <install-setup>` :repo:`fred-utils-pyfco`
  – a Python wrapper over CORBA (used by fred-rdap, fred-webwhois, fred-webadmin)
* :ref:`::S:: <install-setup>` :repo:`fred-utils-pylogger`
  – a Python wrapper over logging infrastructure for all Python clients
  (used by fred-rdap, fred-webwhois, fred-webadmin)

* :ref:`::S:: <install-setup>` :repo:`fred-logger-maintenance`
  – Python scripts for logger (audit log) database maintenance

.. rubric:: PAIN (sample implementation of new billing)

* :ref:`::S:: <install-setup>` :repo:`fred-transproc`
  – a Python script for querying various sources of bank transactions (payments) and processing them with Django PAIN
* :ref:`::S:: <install-setup>` :repo:`django-pain`
  – Django :term:`PAIN` application
* :ref:`::S:: <install-setup>` :repo:`fred-pain`
  – FRED connector plugin for :term:`PAIN` also based on Django
