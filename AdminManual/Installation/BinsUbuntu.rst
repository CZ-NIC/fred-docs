


Installation of binaries on Ubuntu
----------------------------------

This section will guide you through installation of pre-compiled binaries
on Ubuntu.

Before you start, make sure that all :ref:`system requirements <system-reqs>`
are met.

You can install the binaries in two ways:

* download and run our `installation script`_ that will automatically install
  all required components incl. auxiliary software, or
* you can follow the `installation steps`_
  one-by-one manually. The steps describe basically what the script does.

.. Important:: Remember to :ref:`set the timezone in PostgreSQL <set-pg>`
   to ``UTC``, after you complete installation either way.



Installation script
^^^^^^^^^^^^^^^^^^^

To install the FRED and associated software with the installation script,
follow this procedure:

.. code-block:: bash

   # Switch to root
   sudo su -
   # Download the script
   wget -O fred-ubuntu-install.sh https://fred.nic.cz/public/media/1568014036/56/
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

      apt-get --assume-yes install software-properties-common

#. Add the current CZ.NIC signing key to ``apt``

   .. code-block:: bash

      apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1C0200016A9AC5C6

#. Add required repositories

   .. code-block:: bash

      add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) universe multiverse"
      add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc)-updates universe multiverse"
      add-apt-repository "http://archive.nic.cz/ubuntu/"

#. Update ``apt`` index

   .. code-block:: bash

      apt-get update

#. Install the Postfix mail server

   .. code-block:: bash

      # preset Postfix configuration
      debconf-set-selections <<< "postfix postfix/mailname string $(hostname)"
      debconf-set-selections <<< "postfix postfix/main_mailer_type string 'Internet Site'"
      apt-get --assume-yes install postfix

#. Install the FRED package

   .. code-block:: bash

      apt-get --assume-yes install fred

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

#. Some servers require the :ref:`system registrar <system-registrar>`
   to be present in the Registry, before they can be started.

   To quickly create it, use the following command (eventually see
   :ref:`FRED-Admin-reginit-reg`):

   .. code-block:: bash

      fred-admin --registrar_add --handle=REG-SYSTEM --country=CZ --no_vat --system

   The default handle is ``REG-SYSTEM``, but you may use a different handle
   if you specify it in the configuration options ``system_registrar`` and
   ``automatically_managed_keyset_registrar``.

   You don't need to set up EPP access for this registrar, because internal
   administration happens out of EPP.

#. Start the FRED services

   .. code-block:: bash

      service fred-rifd start
      service fred-adifd start
      service fred-pifd start
      service fred-logd start
      service fred-msgd start
      service fred-rsifd start
      service fred-akmd start
      service fred-pyfred start
      service fred-webadmin start

#. Finished.

.. include:: After.rst
