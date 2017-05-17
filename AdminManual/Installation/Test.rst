
.. _FRED-Admin-Install-Test:

Testing the installation
------------------------

Once the installation is finished, you may want to check that it was successful.

There are several levels of testing the installation:

* :ref:`a check of running processes <test-processes>`,
* :ref:`a smoke test <test-smoke>` that will check that all FRED's interfaces
  are correctly configured and responding,
* :ref:`a zone test <test-registrations>` that will check that a registrar
  can access the zone, make registrations and that the registered domain
  is generated into the zone file and available via the public interface.

.. _test-processes:

Check of running processes
^^^^^^^^^^^^^^^^^^^^^^^^^^

The following daemons should start automatically after the FRED was installed:

* fred-adifd
* fred-logd
* fred-msgd
* fred-pifd
* fred-pyfred
* fred-rifd
* fred-webadmin

You can check the running FRED processes with the command ``ps -ef | grep "fred-"``.

.. _test-smoke:

Smoke test of an uninitialized system
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To test the plain installation (just to check that all interfaces respond
as they should), try to open these sites in a browser:

* http://localhost/whois (Web Whois) and attempt a search

   Desired result: loads without errors, search responds with the "Handle not
   found" message without errors

* http://localhost:18456 (Web Admin) and log in with custom username/password
  (e.g. test/test)

   Desired result: loads and logs in without errors

and/or try to run these programs in a terminal:

* ``fred-client -v 2``
   Desired result: outputs Server ID and Return code: 2501
* ``whois -h localhost whatever``
   Desired result: outputs Whoisd server version and ERROR:101
* ``genzone_client whatever``
   Desired result: outputs this error: "Unknown zone requested"

If everything goes smoothly (websites open and programs finish as desired),
then all system interfaces are available.

.. _test-registrations:

Test of registrations in a zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can use the following set of commands to test registrations on your system
after the :ref:`initialization with the config-zone script <init-zone-script>`.

.. TODO Add link to zone semi-automatic initialization with a script

.. code-block:: bash

   # Connect to the server via EPP and login with the specified username and password
   fred-client -u REG-CZ -w passwd
   # Connect + run command that will create a contact with given credentials
   fred-client -u REG-CZ -w passwd -d 'create_contact TEST-CONTACT "Name Surname" email@example.com Street City 12345 CZ'
   # Connect + run command that will create a set of nameservers with the contact assigned as a technical contact
   fred-client -u REG-CZ -w passwd -d 'create_nsset TEST-NSSET ((ns1.test-domain.cz (111.222.111.222)),(ns2.test-domain.cz (222.111.222.111))) TEST-CONTACT'
   # Create a domain with the contact as the domain owner and with the NS set
   fred-client -u REG-CZ -w passwd -d 'create_domain test-domain.cz TEST-CONTACT NULL TEST-NSSET'
   # Ask about the domain via the command-line whois
   whois -h localhost -- test-domain.cz
   # Generate a zone file and check that it contains the domain
   genzone_client; cat db.cz
   # Ask about the domain via RDAP and check the JSON response
   wget -q -O - localhost/rdap/domain/test-domain.cz | json_pp
