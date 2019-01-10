
.. _FRED-Admin-Install-SysInit:

System initialization
---------------------

The system is installed and running, however it still is not fully functional –
domains cannot be registered yet because the database does not contain
any information about zones or registrars. This initial data must be
put in, first.

There are two ways to initialize the system:

* you can run the provided :ref:`config-zone script <init-zone-script>`
  for a quick setup of a single TLD zone – see below, or
* you can use administration tools directly to input custom data
  – this is described in detail in the :doc:`../RegistryInitialization` chapter.

.. _init-zone-script:

Config-zone script
^^^^^^^^^^^^^^^^^^

For a simple setup of your particular TLD, you can download and use
`this Python script <https://fred.nic.cz/files/fred/fred-config-zone.py>`_.

It takes a TLD as an argument and generates a set of shell commands
on std.output, which can be directly executed. Of course, you can have a look
at those commands first to see what they do.

They will configure a zone, setup zero price for registrations and
create one system registrar with the handle ``REG-TLD`` and
EPP password ``passwd``.
Zone SOA parameters are extracted from the real DNS.

Here is an example of usage with the CZ TLD:

.. code-block:: bash
   :caption: Config-zone script usage example

   wget https://fred.nic.cz/files/fred/fred-config-zone.py
   python fred-config-zone.py cz > fred-config-cz.sh
   . fred-config-cz.sh
