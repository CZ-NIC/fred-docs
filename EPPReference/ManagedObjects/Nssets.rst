
.. _mng-nsset:

Nssets
------

A nsset contains information which represents a set of name servers.

Namespace: \http://www.nic.cz/xml/epp/nsset-1.2 |br|
Schema: nsset-1.2.2.xsd

.. _mng-nsset-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, nssets also have
the following attributes:

``id``
   The nsset handle. See :ref:`mngobj-handle-syntax`.

``ns``
   The 2–10 name servers, consisting of:

   ``name``
      Name-server hostname. See :ref:`mngobj-domain-syntax`.

   ``addr``
      Name-server IP address(es). (`Glue record.
      <https://en.wikipedia.org/wiki/Domain_Name_System#Circular_dependencies_and_glue_records>`_)

      At least one IP address must be present if and only if the hostname is in the generated zone.

      Both IPv4 and IPv6 are allowed, accepted in textual representation:

      * The syntax of an IPv4 address:
        Four decimal integers 0–255 separated by periods, leading zeroes are optional.

      * The syntax of an IPv6 address is described in :rfc:`4291#section-2.2`.

      An IP address must not belong to an invalid range.
      See the *Prohibited networks* section in `IANA's Technical requirements
      for authoritative name servers <https://www.iana.org/help/nameserver-requirements>`_.

``tech``
   The :ref:`handle <mngobj-handle-syntax>`\ (s) of 1–10 technical contact(s).

``reportlevel``
   The highest level of technical tests to be performed and reported.
   A higher number means more detail, zero means no tests.

.. _mng-nsset-stat:

Object states
^^^^^^^^^^^^^

A nsset can have one or more of the following statuses:

* ``ok`` – no other states are set
* ``linked`` – the nsset has relation to other records in the Registry
* ``serverDeleteProhibited`` – deletion of the nsset is forbidden
* ``serverTransferProhibited`` – transfer of the nsset is forbidden
* ``serverUpdateProhibited`` – update of the nsset is forbidden
* ``deleteCandidate`` – the nsset is scheduled for deletion

.. _mng-nsset-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`nsset:check </EPPReference/CommandStructure/Check/CheckNsset>`
* :doc:`nsset:create </EPPReference/CommandStructure/Create/CreateNsset>`
* :doc:`nsset:delete </EPPReference/CommandStructure/Delete/DeleteNsset>`
* :doc:`nsset:info </EPPReference/CommandStructure/Info/InfoNsset>`
* :doc:`nsset:transfer </EPPReference/CommandStructure/Transfer/TransferNsset>`
* :doc:`nsset:update </EPPReference/CommandStructure/Update/UpdateNsset>`
* :doc:`nsset:test </EPPReference/CommandStructure/TestNsset>`
* :doc:`nsset:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoNsset>`

.. top-level elements

   * command TLE: ``<nsset:check>``, ``<nsset:create>``, ``<nsset:delete>``,
     ``<nsset:info>``, ``<nsset:transfer>``, ``<nsset:update>``,
     ``<nsset:sendAuthInfo>``, ``<nsset:test>``

   * response data TLE: ``<nsset:chkData>``, ``<nsset:creData>``, ``<nsset:infData>``

   * poll msg TLE: ``<nsset:trnData>``, ``<nsset:idleDelData>``,
     ``<nsset:updateData>``, ``<nsset:testData>``
