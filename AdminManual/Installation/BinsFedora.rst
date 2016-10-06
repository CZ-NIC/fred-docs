


Installation of binaries on Fedora
----------------------------------

This section will guide you through installation of pre-compiled binaries
on Fedora.

Before you start, make sure that all system requirements are met,
see :ref:`System requirements <system-reqs>`.

You can install the binaries by following these installation steps:

.. _install-steps-fedora:

Installation steps
^^^^^^^^^^^^^^^^^^

#. Get information about the FRED repository

   .. code:: bash

      dnf install http://archive.nic.cz/yum/fred/23/x86_64/fred-repo-1.0-1.noarch.rpm

#. Install all FRED packages

   .. code:: bash

      dnf install fred-*

#. Install the database schema

   The setup script installs table schemas and fills enumeration tables;
   it does NOT initialize the system with basic data – that is described
   in the :ref:`System initialization <FRED-Admin-Install-SysInit>` section.

   .. code:: bash

      /usr/bin/postgresql-setup initdb

#. Start services

   .. code:: bash

      service postgresql start
      service omniNames start
      service fred-server start
      service httpd start
      service fred-webadmin-server start

#. Finished. You can :ref:`test the installation <FRED-Admin-Install-Test>` now.

.. Note::

   Before you start using the system, you must
   :ref:`initialize <FRED-Admin-Install-SysInit>` it.
