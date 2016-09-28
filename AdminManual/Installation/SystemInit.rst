
.. _FRED-Admin-Install-SysInit:

System initialization
---------------------

The system is installed and running, however it still is not fully functional –
domains can not be registered yet because the database does not contain
any information about zones or registrars. This initial data must be
put in, first.

There are several ways to initialize the system:

* you can run a script to fill the system with the data of the :ref:`Czech environment <init-czech>` (for testing purposes only),
* you can run a :ref:`script for a quick setup <init-zone-script>` of a single TLD zone, or
* you can use administration tools to input custom data – this is described in detail in the :ref:`Registry initialization <FRED-Admin-RegInit>` chapter.

.. _init-czech:

Czech environment data
^^^^^^^^^^^^^^^^^^^^^^

To initialize the registry with the testing data of the Czech environment,
run this script:

.. code:: bash

   sudo su - postgres -c "/usr/sbin/fred-dbinit-cztest"

The script does not take any arguments, it just provides some basic static data for testing:

   * adds SOA parameters for zones "cz" and "0.2.4.e164.arpa"
   * adds zone nameservers for both zones
   * adds 2 testing (non-system) registrars: REG-FRED_A and REG-FRED_B
   * assigns them EPP authentication data (password: ``passwd``)
   * grants access to both zones to the both registrars
   * changes some parameters in the database (see :ref:`Configurable database values <TODO-LINK>`)

What the script "forgets" to do:

   * set price list,
   * create the system registrar

.. only:: mode_structure

   .. todo:: Why the :program:`fred-dbinit-cztest` script does not set a sample price list anymore?

.. _init-zone-script:

Config-zone script
^^^^^^^^^^^^^^^^^^

For a simple setup of your particular TLD, you can download and use
`this Python script <https://fred.nic.cz/files/fred/fred-config-zone.py>`_.

It takes just the TLD as an argument and generates a set of shell commands
on std.output that can be directly executed. Of course, you can have a look
at those commands first to see what they do.

They will configure a zone, setup zero price for registrations and
create one system registrar with the handle ``REG-TLD`` and
EPP password ``passwd``.
Zone SOA parameters are extracted from the real DNS.

Here is an example of usage with the CZ zone:

.. code:: bash

   wget https://fred.nic.cz/files/fred/fred-config-zone.py
   python fred-config-zone.py cz > fred-config-cz.sh
   . fred-config-cz.sh

Custom init
^^^^^^^^^^^

If you want to initialize the system completely by yourself,
see :ref:`Registry initialization <FRED-Admin-RegInit>`.
