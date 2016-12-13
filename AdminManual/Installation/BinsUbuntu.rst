


Installation of binaries on Ubuntu
----------------------------------

This section will guide you through installation of pre-compiled binaries
on Ubuntu.

Before you start, make sure that all system requirements are met,
see :ref:`System requirements <system-reqs>`.

You can install the binaries in two ways:

* download and run our `installation script`_ that will take care
  of everything that needs to be done, or
* you can follow the `installation steps <install-steps-ubuntu>`_
  one-by-one manually. The steps basically describe what the script does.

.. Note:: During installation, you will be prompted about Postfix configuration
   and MS core fonts license agreement.

Installation script
^^^^^^^^^^^^^^^^^^^

To install the FRED and associated software with the installation script,
follow this procedure:

.. code:: bash

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

   .. code:: bash

      sudo su -

#. Enable the `add-apt-repository` command

   .. code:: bash

      apt-get install software-properties-common

#. Add required repositories

   .. code:: bash

      add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) universe multiverse"
      add-apt-repository "http://archive.nic.cz/ubuntu/"

#. Add the CZ.NIC signing key to ``apt`` and update ``apt`` index

   .. code:: bash

      apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F20C079E020ADBB4
      apt-get update

#. Install the Postfix mail server

   .. code:: bash

      apt-get install postfix

3. Install the FRED package with all dependencies

   .. code:: bash

      apt-get install fred

#. Install the database schema of the FRED

   The *db manager* installs table schemas and fills enumeration tables;
   it does NOT initialize the system with basic data – the latter is described
   in the :ref:`System initialization <FRED-Admin-Install-SysInit>` section.

   .. code:: bash

      su - postgres -c "/usr/sbin/fred-dbmanager install"

#. Enable the FRED sites in Apache and reload configuration

   .. code:: bash

      a2ensite 02-fred-mod-eppd-apache.conf
      a2ensite 02-fred-mod-whoisd-apache.conf
      a2ensite 03-fred-whois.conf
      a2ensite rdap.conf
      service apache2 reload

#. Start the FRED services

   .. code:: bash

      service fred-rifd start
      service fred-adifd start
      service fred-pifd start
      service fred-logd start
      service fred-msgd start
      service fred-pyfred start
      service fred-webadmin start

#. Replace `mpm-event` with `mpm-prefork` in Apache and restart

   .. Note:: This is a workaround for Ubuntu 14.04 and 16.04.

      The `mod-whoisd` module is not compatible with the `mpm-event`
      Apache scheme that is installed by default, so it must be
      disabled and replaced with `mpm-prefork`.

   .. todo:: Apache workaround should be conditional
      in the install script.

   .. code:: bash

      apt-get install apache2-mpm-prefork # only 14.04
      a2dismod mpm_event
      a2enmod mpm_prefork
      service apache2 restart

#. Finished. You can :ref:`test the installation <FRED-Admin-Install-Test>` now.

.. Note::

   Before you start using the system, you must
   :ref:`initialize <FRED-Admin-Install-SysInit>` it.
