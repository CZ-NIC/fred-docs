


Installation of binaries on Fedora or RHEL/CentOS
-------------------------------------------------

This section will guide you through installation of pre-compiled binaries
on Fedora or RHEL/CentOS systems.

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
   wget https://fred.nic.cz/files/fred/fred-rh-install.sh
   # Execute the script
   . fred-rh-install.sh

What steps the script takes is explained in the following section.

.. _install-steps-fedora:

Installation steps
^^^^^^^^^^^^^^^^^^

#. Configure the FRED repository (and install auxiliary software, respectively)

   a) Fedora

      .. code-block:: bash

         dnf config-manager --add-repo http://archive.nic.cz/yum/fred/fedora/fred.repo

   b) RHEL/CentOS

      .. code-block:: bash

         yum install -y yum-utils
         if cat /etc/redhat-release | grep -q Enterprise
         then
            yum-config-manager --enable rhel-7-server-optional-rpms rhel-7-server-extras-rpms
         fi
         # config fred repository
         yum-config-manager --add-repo http://archive.nic.cz/yum/fred/epel/fred.repo
         # install repository with dependecies
         yum install -y  https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
         # install new postgresql
         yum install -y https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-redhat96-9.6-3.noarch.rpm
         yum install -y postgresql96-server
         ln -s /usr/pgsql-9.6/bin/pg_ctl /usr/bin/pg_ctl
         ln -s /usr/pgsql-9.6/bin/postgresql96-setup /usr/bin/postgresql-setup
         ln -s /var/lib/pgsql/9.6/data/ /var/lib/pgsql/
         ln -s /usr/lib/systemd/system/postgresql-9.6.service /usr/lib/systemd/system/postgresql.service

#. Install all FRED packages

   a) Fedora

      .. code-block:: bash

         dnf install -y 'fred-*' -x '*debug*'

   b) RHEL/CentOS

      .. code-block:: bash

         yum install -y 'fred-*' -x '*debug*'

#. Install the database schema

   The setup script installs table schemas and fills enumeration tables;
   it does NOT initialize the system with basic data – the latter is described
   in the :ref:`System initialization <FRED-Admin-Install-SysInit>` section.

   .. code-block:: bash

      /usr/bin/postgresql-setup initdb
      systemctl start postgresql
      su - postgres -c "/usr/sbin/fred-dbmanager install"

#. Start services

   .. code-block:: bash

      systemctl start omniNames
      systemctl start fred-rifd
      systemctl start fred-adifd
      systemctl start fred-pifd
      systemctl start fred-logd
      systemctl start fred-msgd
      systemctl start fred-rsifd
      systemctl start fred-pyfred
      systemctl start fred-webadmin
      systemctl start httpd

   .. Note:: Sometimes :file:`/run/uwsgi` is not created; in that case,
      create it manually:

      .. code-block:: bash

         test -d /run/uwsgi/ && echo "/run/uwsgi exists" || {
            echo "/run/uwsgi missing so creating"
            install -o uwsgi -g uwsgi -d /run/uwsgi
         }
         systemctl start uwsgi

#. Finished.

After installation
^^^^^^^^^^^^^^^^^^

Check and adapt, respectively, the :doc:`system configuration <../Configuration>`.

Before registrars can access the Registry, you must :doc:`initialize <SystemInit>` it.

You may also want to :doc:`test the installation <Test>`.
