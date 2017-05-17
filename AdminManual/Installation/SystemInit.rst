
.. _FRED-Admin-Install-SysInit:

System initialization
---------------------

The system is installed and running, however it still is not fully functional –
domains cannot be registered yet because the database does not contain
any information about zones or registrars. This initial data must be
put in, first.

There are two ways to initialize the system:

* you can run a :ref:`script for a quick setup <init-zone-script>` of a single
  TLD zone, or
* you can use administration tools directly to input custom data
  – this is described in detail in the :ref:`Registry initialization
  <FRED-Admin-RegInit>` chapter.

.. _init-zone-script:

Config-zone script
^^^^^^^^^^^^^^^^^^

For a simple setup of your particular TLD, you can download and use
`this Python script <https://fred.nic.cz/files/fred/fred-config-zone.py>`_.

It takes just the TLD as an argument and generates a set of shell commands
on std.output that can be directly executed. Of course, you can have a look
at those commands first to see what they do.

They will configure a zone, setup zero price for registrations and
create one system registrar with the handle ``REG-TLD`` and
EPP password ``passwd``.
Zone SOA parameters are extracted from the real DNS.

Here is an example of usage with the CZ zone:

.. code-block:: bash

   wget https://fred.nic.cz/files/fred/fred-config-zone.py
   python fred-config-zone.py cz > fred-config-cz.sh
   . fred-config-cz.sh

Custom init
^^^^^^^^^^^

If you want to initialize the system completely by yourself,
see :ref:`Registry initialization <FRED-Admin-RegInit>`.
