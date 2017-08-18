
.. _mng-nsset:

Nssets
------

A group of name servers.

Namespace: \http://www.nic.cz/xml/epp/nsset-1.2 |br|
Schema: nsset-1.2.2.xsd

.. top-level elements

   * command TLE: ``<nsset:check>``, ``<nsset:create>``, ``<nsset:delete>``,
     ``<nsset:info>``, ``<nsset:transfer>``, ``<nsset:update>``,
     ``<nsset:sendAuthInfo>``, ``<nsset:test>``

   * response data TLE: ``<nsset:chkData>``, ``<nsset:creData>``, ``<nsset:infData>``

   * poll msg TLE: ``<nsset:trnData>``, ``<nsset:idleDelData>``,
     ``<nsset:updateData>``, ``<nsset:testData>``

.. _mng-nsset-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, nssets also have
the following attributes:

id
   The nsset handle. See :ref:`mngobj-handle-syntax`.

ns
   The nameserver(s), consisting of:

   name
      Nameserver hostname. See :ref:`mngobj-domain-syntax`.

   addr
      Nameserver IP address(es). (Glue.)

      At least one IP address must be present if and only if the hostname is in the generated zone.

      Both IPv4 and IPv6 are allowed, accepted in textual representation:

      * The syntax of an IPv4 address:
        Four decimal numbers (0–255) separated by periods, leading zeroes are optional.

      * The syntax of an IPv6 address:
        Eight hexadecimal numbers (0000–ffff) separated by colons,
        leading zeroes are optional. Two consecutive zero groups can be collapsed
        into ``::`` but this can appear only once in an address.
        See :rfc:`4291#section-2.2`.

      An IP address must not belong to an invalid range.
      See the *Prohibited networks* section in `IANA's Technical requirements
      for authoritative name servers <https://www.iana.org/help/nameserver-requirements>`_.

tech
   The :ref:`handle <mngobj-handle-syntax>`\ (s) of technical contact(s).

reportlevel
   The highest level of technical tests to be performed and reported.
   A higher number is more detail, zero means no tests???.

.. _mng-nsset-stat:

Object states
^^^^^^^^^^^^^

A nsset can have one or more of the following statuses:

* ``ok`` – no other states are set
* ``linked`` – the nsset has relation to other records in the Registry
* ``serverDeleteProhibited`` – deletion of the nsset is forbidden
* ``serverTransferProhibited`` – transfer of the nsset is forbidden
* ``serverUpdateProhibited`` – update of the nsset is forbidden
* ``deleteCandidate`` – the nsset is scheduled for deletion

.. _mng-nsset-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`nsset:check </EPPReference/CommandStructure/Check/CheckNsset>`
* :doc:`nsset:create </EPPReference/CommandStructure/Create/CreateNsset>`
* :doc:`nsset:delete </EPPReference/CommandStructure/Delete/DeleteNsset>`
* :doc:`nsset:info </EPPReference/CommandStructure/Info/InfoNsset>`
* :doc:`nsset:transfer </EPPReference/CommandStructure/Transfer/TransferNsset>`
* :doc:`nsset:update </EPPReference/CommandStructure/Update/UpdateNsset>`
* :doc:`nsset:test </EPPReference/CommandStructure/TestNsset>`
* :doc:`nsset:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoNsset>`
