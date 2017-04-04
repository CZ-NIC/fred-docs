


Installation of binaries on Fedora or RHEL/Centos
-------------------------------------------------

This section will guide you through installation of pre-compiled binaries
on Fedora or RHEL/Centos systems.

Before you start, make sure that all system requirements are met,
see :ref:`System requirements <system-reqs>`.

.. Important:: Remember to :ref:`set the timezone in PostgreSQL <set-pg>`
   to ``UTC``.

You can install the binaries by following these installation steps:

.. _install-steps-fedora:

Installation steps
^^^^^^^^^^^^^^^^^^

#. Get information about the FRED repository

   .. code-block:: bash

      dnf config-manager --add-repo http://archive.nic.cz/yum/fred/fedora/fred.repo
      # in case of Redhat/Centos 7 enable epel and use yum
      # yum install epel-release
      # yum-config-manager --add-repo http://archive.nic.cz/yum/fred/epel/fred.repo
      
#. Install all FRED packages

   .. code-block:: bash

      dnf install fred-*
      # in case of Redhat/Centos use yum
      # yum install fred-*

#. Install the database schema

   The setup script installs table schemas and fills enumeration tables;
   it does NOT initialize the system with basic data – the latter is described
   in the :ref:`System initialization <FRED-Admin-Install-SysInit>` section.

   .. code-block:: bash

      /usr/bin/postgresql-setup initdb

#. Start services

   .. code-block:: bash

      service postgresql start
      service omniNames start
      service fred-server start
      service httpd start
      service fred-webadmin-server start

#. Finished. You can :ref:`test the installation <FRED-Admin-Install-Test>` now.

.. Note::

   Before you start using the system, you must
   :ref:`initialize <FRED-Admin-Install-SysInit>` it.
