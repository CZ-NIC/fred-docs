
.. _mng-keyset:

Keysets
-------

A keyset contains information which represents a set of DNSSEC keys.

Namespace: \http://www.nic.cz/xml/epp/keyset-1.3 |br|
Schema: keyset-1.3.2.xsd

.. Note:: DNSSEC keys mapping is partially based on the standard :rfc:`5910`
   but implemented with the following modifications:

   * keys are grouped in a set that is identified by a handle,
   * a standalone object instead of just a domain extension,
   * custom element structure for DNSSEC key representation,
   * association with technical contacts.

.. _mng-keyset-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, keysets also have
the following attributes:

``id``
   The keyset handle. See :ref:`mngobj-handle-syntax`.

``dnskey``
   The 1–10 DNSSEC key(s), consisting of:

   ``flags``
      Flags. Allowed values are: ``0``, ``256``, ``257``.

   ``protocol``
      Protocol. The only allowed value is ``3``.

   ``alg``
      Algorithm number defined by IANA, see `DNS Security Algorithm Numbers
      <https://www.iana.org/assignments/dns-sec-alg-numbers/dns-sec-alg-numbers.xhtml#dns-sec-alg-numbers-1>`_.

      The FRED EPP server does not allow to use ``0``, ``1``, ``2`` and ``252`` by default.

   ``pubKey``
      Public key as :term:`keyset:keyT`.

   .. Note:: A DNSSEC key corresponds to a DNSKEY Resource Record,
      see :rfc:`4034#section-2`.

``tech``
   The :ref:`handle <mngobj-handle-syntax>`\ (s) of 1–10 technical contact(s).

.. _mng-keyset-stat:

Object states
^^^^^^^^^^^^^^^^^

A keyset can have one or more of the following statuses:

* ``ok`` – no other states are set
* ``linked`` – the keyset has relation to other records in the Registry
* ``serverDeleteProhibited`` – deletion of the keyset is forbidden
* ``serverTransferProhibited`` – transfer of the keyset is forbidden
* ``serverUpdateProhibited`` – update of the keyset is forbidden
* ``deleteCandidate`` – the keyset is scheduled for deletion

.. _mng-keyset-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`keyset:check </EPPReference/CommandStructure/Check/CheckKeyset>`
* :doc:`keyset:create </EPPReference/CommandStructure/Create/CreateKeyset>`
* :doc:`keyset:delete </EPPReference/CommandStructure/Delete/DeleteKeyset>`
* :doc:`keyset:info </EPPReference/CommandStructure/Info/InfoKeyset>`
* :doc:`keyset:transfer </EPPReference/CommandStructure/Transfer/TransferKeyset>`
* :doc:`keyset:update </EPPReference/CommandStructure/Update/UpdateKeyset>`
* :doc:`keyset:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoKeyset>`

.. top-level elements:

   * command TLE: ``<keyset:check>``, ``<keyset:create>``, ``<keyset:delete>``,
     ``<keyset:info>``, ``<keyset:transfer>``, ``<keyset:update>``,
     ``<keyset:sendAuthInfo>``, ``<keyset:test>``

   * response data TLE: ``<keyset:chkData>``, ``<keyset:creData>``,
     ``<keyset:infData>``

   * poll msg TLE: ``<keyset:trnData>``, ``<keyset:idleDelData>``,
     ``<keyset:updateData>``, ``<keyset:testData>``
