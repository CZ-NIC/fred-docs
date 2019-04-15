
.. _FRED-Admin-Install-Source:

Installation from source tarballs
---------------------------------

This section will guide you through the compilation of the FRED and
the follow-up installation. This procedure is meant for Ubuntu.

See also :doc:`source code architecture </Architecture/SourceCode>`.

.. Important:: Remember to :ref:`set the timezone in PostgreSQL <set-pg>`
   to ``UTC``.



Add the CZ.NIC signing key and repositories
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

   apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1C0200016A9AC5C6

   add-apt-repository "deb http://archive.nic.cz/ubuntu $(lsb_release -sc) main"
   add-apt-repository "deb http://archive.nic.cz/private $(lsb_release -sc) main"

   apt-get update

Satisfy dependecies
^^^^^^^^^^^^^^^^^^^

We prepared lists of all particular packages on which FRED's compilation,
installation or operation depends (package names may slightly differ
across OS versions):

* :ref:`Ubuntu 14.04 LTS <Source-Deps-Ubu14>`
* :ref:`Ubuntu 16.04 LTS <Source-Deps-Ubu16>`

Install all the packages from the appropriate list.

.. IDEA Separate dependencies for compilation, installation and operation.
   Advantage?


Download and unpack
^^^^^^^^^^^^^^^^^^^

We publish a list of GitHub-generated tarballs `on the website
<https://fred.nic.cz/page/3612/get-fred/>`_.

You may use the `latest version list <https://fred.nic.cz/files/fred/fred-sources-list-latest.txt>`_
or an archived version list (see the website for archived versions).

.. code-block:: bash

   mkdir fred && cd fred
   curl https://fred.nic.cz/files/fred/fred-sources-list-latest.txt | while read LN; do
      curl -JLO $LN # these options are necessary to have nice filenames
   done
   for F in *.tar.gz; do tar -zxvf $F; done

.. _install-auto:

Install "A" packages
^^^^^^^^^^^^^^^^^^^^
These packages are configured, compiled and installed using **Autotools** [#]_
(autoconf, automake and libtool).

IDL definitions are required during compilation, therefore the IDL package
must be installed before other "A" packages and before the :file:`fred-pyfred`
"D" package.

Package list:

* :file:`fred-idl` -- *install first!*
* :file:`fred-mod-corba`
* :file:`fred-mod-eppd`
* :file:`fred-mod-whoisd`
* :file:`fred-server`
* :file:`fred-db`
* :file:`fred-akm`
* :file:`cdnskey-scanner`

For each package in the list, run this command sequence from its directory:

.. code-block:: bash

   autoreconf -vfi # generates the configure script
   ./configure
   make
   sudo make install

The ``configure`` script prepares package files for compilation and
installation by adapting them to a specific environment and checks
that the required tools are available.

The ``make`` command performs
the actual compilation. (Some packages have nothing to compile. In that case,
the ``make`` reports "Nothing to be done...".)

The last command just copies
files required for operation to the target directories. (You usually need
administrator permissions if you install somewhere else than to your home
directory.)

The target directory (installation prefix), as well as other parameters
(e.g. compilation params), can be passed as arguments directly
to the :program:`configure` script or as environment variables.
(See ``./configure --help`` for options.)

.. Note:: Note that the default prefix is used in examples
   throughout this manual.

.. [#] For more information about Autotools see
   the `GNU Automake Manual <http://www.gnu.org/software/automake/manual/>`_.

Finish ``mod-corba`` installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Run the :program:`libtool` script (after ``make install``) to finish
the :file:`mod-corba` installation:

.. code-block:: bash

   sudo ./libtool --finish /usr/lib/apache2/modules

.. _install-dist:

Install "D" packages
^^^^^^^^^^^^^^^^^^^^

These packages use **Distutils** for installation which is a collection
of Python scripts based on **Setuptools**, therefore
the Distutils package must be installed before other "D" packages.
Naturally, Setuptools must be installed (:file:`python-setuptools` or
:code:`pip install setuptools`) before all other Python packages.

Package list:

* :file:`fred-utils-distutils` -- *install first! (in the Python path)*
* :file:`fred-utils-pyfco` [#s]_
* :file:`fred-utils-pylogger` [#s]_
* :file:`fred-client`
* :file:`fred-doc2pdf` [#s]_
* :file:`fred-pyfred`
* :file:`fred-rdap` [#s]_
* :file:`fred-transproc` [#s]_
* :file:`fred-webadmin`
* :file:`fred-webwhois` [#s]_
* :file:`fred-logger-maintenance` [#s]_ (optional)

For each package in the list, run this command from its directory:

.. code-block:: bash

   sudo python ./setup.py install

The ``install`` command calls compilation (build) first if needed and
then just copies files required for operation to the target directories.
(You usually need administrator permissions if you install elsewhere
than your home directory.)

The target directory (installation prefix) or other parameters can be
passed as arguments. Refer to ``python ./setup.py --help install``
for installation parameters.

The installer writes a list of installed files (with their full path)
to the :file:`install.log` file when it finishes.

.. [#s] These packages have been ported from Distutils to Setuptools
   but they have the same installation command, except it does not install
   a configuration file and the package must be configured as described
   in a README file included in the package.

Finalization
^^^^^^^^^^^^

You need to finish the setup of the following parts to make
the system operational:

* enable Apache modules,
* setup the database schema,
* launch servers.

Enable Apache modules
~~~~~~~~~~~~~~~~~~~~~

Enable :file:`mod_ssl` (not enabled by default)::

   sudo a2enmod ssl

Configure Apache to load :file:`mod_eppd` and :file:`mod_whoisd`,
create virtual hosts to provide EPP server and Web Whois server and
configure directories to provide Unix Whois and RDAP server:

* Correct RDAP Apache module configuration (comment or delete
  the ``WSGISocketPrefix`` directive)::

   sudo sed -i~ -e "s/^WSGISocketPrefix/#WSGISocketPrefix/" \
      /usr/local/share/fred-rdap/apache.conf

* Link configuration snippets (provided with the FRED) to Apache's virtual
  host directory::

   cd /etc/apache2/sites-available/
   sudo ln -s /usr/local/share/fred-mod-corba/01-fred-mod-corba-apache.conf .
   sudo ln -s /usr/local/share/fred-mod-whoisd/02-fred-mod-whoisd-apache.conf .
   sudo ln -s /usr/local/share/fred-mod-eppd/02-fred-mod-eppd-apache.conf .
   sudo ln -s /usr/local/share/doc/fred-whois/apache.conf 03-fred-whois.conf
   sudo ln -s /usr/local/share/fred-rdap/apache.conf 04-fred-rdap.conf

* Enable FRED sites::

   sudo a2ensite 01-fred-mod-corba-apache.conf
   sudo a2ensite 02-fred-mod-whoisd-apache.conf
   sudo a2ensite 02-fred-mod-eppd-apache.conf
   sudo a2ensite 03-fred-whois.conf
   sudo a2ensite 04-fred-rdap.conf

* Set the Apache user (www-data) as the owner of the log directory
  to make logging possible::

   sudo chown www-data:www-data /usr/local/var/log/

* Finally, restart the Apache to load the new settings::

   sudo service apache2 restart

.. FRED's Homepage
   ~~~~~~~~~~~~~~~
   localhost -> ``/var/www/index.html``

.. FRED should contain its own index page with links to services
   in the default setup.
   The ``fred-manager`` (http://archive.nic.cz/fred-sources/fred-manager)
   knows to create one but this is not a tool that is publicly available.
..

Setup the database schema
~~~~~~~~~~~~~~~~~~~~~~~~~
.. To install the FRED database schema, run this command::
   sudo su - postgres -c "/usr/local/sbin/fred-dbmanager install"
   dbmanager creates dbuser, db and installs the structure,
   but these variables are embedded in the SQL script and can't be parametrized
   in an other way than compilation of the fred-db package

The FRED database schema is installed automatically with the default settings
 (user name and database name) on the first run of the CORBA servers.

However, if you want to setup the database manually, you need to:

* disable the auto-install by setting the flag ``DB_INIT=0``
  in :file:`/usr/local/etc/init.d/fred-server`
* setup the database settings (as the *postgres* user)::

   su - postgres

  - create a user and set his privileges::

      createuser -SDR -l {dbusername}

  - create a database, set the owner and encoding::

      createdb {dbname} -O {dbusername} -E UTF8

  - install 'plpgsql' language for the database::

      createlang plpgsql {dbname}

  - set a password for the user (from the psql console)::

      psql
      postgres=# alter user {dbusername} password 'passwd';

* adapt the PostgreSQL `client authentication
  <http://www.postgresql.org/docs/current/static/client-authentication.html>`_
  configuration in :file:`/etc/postgresql/9.1/main/pg_hba.conf`
  to use the plain-password authentication method [#]_

   - for all databases and users::

      #TYPE   DATABASE    USER        ADDRESS      *METHOD*
      local   all         all                      password
      host    all         all         127.0.0.1/32 password
      host    all         all         ::1/128      password

   - for your user and your database specifically::

      # Unix-socket connections
      local  {dbname}    {dbusername}              password
      # localhost TCP/IP-socket connections, IPv4
      host   {dbname}    {dbusername} 127.0.0.1/32 password
      # localhost TCP/IP-socket connections, IPv6
      host   {dbname}    {dbusername} ::1/128      password

   - and restart the PostgreSQL server::

      sudo service postgresql restart

.. [#] We use the plain-password method only as an illustration of simple
   settings, however we do not suggest that this method is secure.
   We recommend you to consult the PostgreSQL documentation and your
   local security policy.

* run the provided SQL script to create the FRED database structure::

      psql {dbname} -U {dbusername} -f /usr/local/share/fred-db/structure.sql

* adapt the FRED configuration files accordingly
  (set the correct database name, user and password)

   - :file:`/usr/local/etc/fred/server.conf`::

      [database]
      host = localhost    # hostname of the database server (default)
      port = 5432         # port of the db service (default)
      name = {dbname}     # database name
      user = {dbusername} # database user name
      password = passwd   # user password
      ...

   - :file:`/usr/etc/fred/pyfred.conf`::

      [General]
      ...
      dbuser={dbusername}
      dbname={dbname}
      dbhost=localhost
      dbport=5432
      dbpassword=passwd
      ...



Launch servers
~~~~~~~~~~~~~~
To start the FRED CORBA servers, you can use the :program:`service` script
or run this command:

::

   sudo /usr/local/etc/init.d/fred-server start

To start the FRED webadmin server (Daphne), you can use the :program:`service`
script or run this command:
::

   sudo /usr/etc/init.d/fred-webadmin-server start

.. NOTE bad prefix reported in Trac ticket #13929

Now, you can perform :ref:`the smoke test <test-smoke>` to make sure
that all interfaces are available and working together.

.. todo:: how to create service(s) and add it(them) to startup launch
   :class: todo-backlog

.. include:: After.rst
