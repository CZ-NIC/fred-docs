


Installation of binaries on Ubuntu
----------------------------------

This section will guide you through installation of pre-compiled binaries
on Ubuntu.

Before you start, make sure that all system requirements are met,
see :ref:`System requirements <system-reqs>`.

You can install the binaries in two ways:

* download and run our `installation script`_ that will take care
  of everything that needs to be done, or
* you can follow the :ref:`installation steps <install-steps-ubuntu>`
  one-by-one manually. The steps basically describe what the script does.

.. Note:: During installation, you will be prompted about Postfix configuration
   and MS core fonts license agreement.

.. Important:: Remember to :ref:`set the timezone in PostgreSQL <set-pg>`
   to ``UTC``.



Installation script
^^^^^^^^^^^^^^^^^^^

To install the FRED and associated software with the installation script,
follow this procedure:

.. code-block:: bash

   # Switch to root
   sudo su -
   # Download the script
   wget https://fred.nic.cz/files/fred/fred-ubuntu-install.sh
   # Execute the script
   . fred-ubuntu-install.sh

What steps the script takes is explained in the following section.

.. _install-steps-ubuntu:

Installation steps
^^^^^^^^^^^^^^^^^^

This section explains the individual steps that are taken by the installation
script to install software required for the operation of the FRED.

#. Switch to root before you begin

   .. code-block:: bash

      sudo su -

#. Enable the ``add-apt-repository`` command

   .. code-block:: bash

      apt-get install software-properties-common

#. Add required repositories

   .. code-block:: bash

      add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) universe multiverse"
      add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc)-updates universe multiverse"
      add-apt-repository "http://archive.nic.cz/ubuntu/"

#. Add the CZ.NIC signing key to ``apt`` and update ``apt`` index

   .. code-block:: bash

      apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1C0200016A9AC5C6
      apt-get update

#. Install the Postfix mail server

   .. code-block:: bash

      apt-get install postfix

#. Install the FRED package

   .. code-block:: bash

      apt-get install fred

#. Install the database schema of the FRED

   The :program:`fred-dbmanager` installs table schemas and fills enumeration
   tables;
   it does NOT initialize the system with basic data – the latter is described
   in the :ref:`System initialization <FRED-Admin-Install-SysInit>` section.

   .. code-block:: bash

      su - postgres -c "/usr/sbin/fred-dbmanager install"

#. Enable FRED sites in UWSGI

   .. code-block:: bash

      ln -s /etc/uwsgi/apps-available/fred-rdap.ini /etc/uwsgi/apps-enabled/
      ln -s /etc/uwsgi/apps-available/fred-webwhois.ini /etc/uwsgi/apps-enabled/
      service uwsgi restart

#. Enable FRED sites in Apache

   .. code-block:: bash

      a2ensite 02-fred-mod-eppd-apache.conf
      a2ensite 02-fred-mod-whoisd-apache.conf
      a2enconf fred-rdap.conf
      a2enconf fred-webwhois.conf

#. Replace ``mpm-event`` with ``mpm-prefork`` in Apache and restart

   .. Note:: This is a workaround for Ubuntu 16.04.

      The ``mod-whoisd`` module is not compatible with the ``mpm-event``
      Apache scheme that is installed by default, so it must be
      disabled and replaced with ``mpm-prefork``.

   .. code-block:: bash

      a2dismod mpm_event
      a2enmod mpm_prefork
      service apache2 restart

#. Start the FRED services

   .. code-block:: bash

      service fred-rifd start
      service fred-adifd start
      service fred-pifd start
      service fred-logd start
      service fred-msgd start
      service fred-rsifd start
      service fred-pyfred start
      service fred-webadmin start

#. Finished. You can :ref:`test the installation <FRED-Admin-Install-Test>` now.

.. Note::

   Before you start using the system, you must
   :ref:`initialize <FRED-Admin-Install-SysInit>` it.
