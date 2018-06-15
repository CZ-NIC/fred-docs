
.. _mng-domain:

Domains
-------

A domain contains information which represents a regular domain or
an :term:`ENUM` domain.

Namespace: \http://www.nic.cz/xml/epp/domain-1.4 |br|
Schema: domain-1.4.2.xsd

.. Note:: Domain name mapping is based on the standard :rfc:`5731`
   but implemented with the following modifications:

   * replacement of a list of name servers with an nsset,
   * addition of a keyset,
   * simplification of the list of contacts to just one type of contact (admin).

.. _mng-domain-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, domains also have
the following attributes:

``name``
   The domain name. See :ref:`mngobj-domain-syntax`.

``registrant``
   The :ref:`handle <mngobj-handle-syntax>` of the domain owner contact.

``admin``
   The :ref:`handle <mngobj-handle-syntax>`\ (s) of zero or more administrative contact(s).

``nsset``
   The :ref:`handle <mngobj-handle-syntax>` of a nameserver set.

``keyset``
   The :ref:`handle <mngobj-handle-syntax>` of a DNSSEC-key set.

``exDate``
   The date of domain name expiration.

``valExDate`` :sup:`ENUM extension`
   The date of the expiration of ENUM domain validation.

``publish`` :sup:`ENUM extension` :sup:`+ DEPRECATED`
   Flag of publishing an ENUM domain in a public ENUM directory.

   This attribute has currently no meaning for the server and it will be removed
   in the future. Use of this attribute is discouraged.

.. _mng-domain-stat:

Object states
^^^^^^^^^^^^^^^^^

A domain can have one or more of the following statuses:

* ``ok`` – no other states are set
* ``serverDeleteProhibited`` – deletion of the domain is forbidden
* ``serverRenewProhibited`` – renewal of the domain is forbidden
* ``serverTransferProhibited`` – transfer of the domain is forbidden
* ``serverUpdateProhibited`` – update of the domain is forbidden
* ``serverRegistrantChangeProhibited`` – the change of the registrant of the domain is forbidden
* ``serverBlocked`` – the domain is blocked by administration
* ``serverOutzoneManual`` – domain's absence in the zone is forced by administration
* ``serverInzoneManual`` – domain's presence in the zone is forced by administration
* ``expired`` – the domain is expired
* ``outzone`` – the domain is not included in the zone
* ``notValidated`` :sup:`ENUM only` – the ENUM domain is not validated
* ``deleteCandidate`` – the domain is scheduled for deletion

.. _mng-domain-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`domain:check </EPPReference/CommandStructure/Check/CheckDomain>`
* :doc:`domain:create </EPPReference/CommandStructure/Create/CreateDomain>`
* :doc:`domain:delete </EPPReference/CommandStructure/Delete/DeleteDomain>`
* :doc:`domain:info </EPPReference/CommandStructure/Info/InfoDomain>`
* :doc:`domain:renew </EPPReference/CommandStructure/RenewDomain>`
* :doc:`domain:transfer </EPPReference/CommandStructure/Transfer/TransferDomain>`
* :doc:`domain:update </EPPReference/CommandStructure/Update/UpdateDomain>`
* :doc:`domain:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoDomain>`

.. top-level elements

   command TLE: ``<domain:check>``, ``<domain:create>``, ``<domain:delete>``,
   ``<domain:info>``, ``<domain:renew>``, ``<domain:transfer>``, ``<domain:update>``,
   ``<domain:sendAuthInfo>`` :sup:`EXT`

   response data TLE: ``<domain:chkData>``, ``<domain:creData>``, ``<domain:infData>``,
   ``<domain:renData>``

   poll msg TLE: ``<domain:trnData>``, ``<domain:impendingExpData>``, ``<domain:expData>``,
   ``<domain:dnsOutageData>``, ``<domain:delData>``, ``<domain:updateData>``

   ENUM poll msg TLE: ``enumval:impendingValExpData``, ``enumval:valExpData``

.. _mng-domain-ext:

ENUM domains
^^^^^^^^^^^^

ENUM domains have the same set of attributes as regular domains except for two
additional attributes. Therefore they are managed by the same commands &
responses as regular domains, only the handling of the additional attributes
requires :doc:`extensions of the standard commands & responses
</EPPReference/ProtocolBasics/ComResExtensions>`,
so that these attributes can be included in transactions where appropriate.

Namespace: \http://www.nic.cz/xml/epp/enumval-1.2 |br|
Schema: enumval-1.2.0.xsd

These extensions are used with the following commands:

* :doc:`domain:create </EPPReference/CommandStructure/Create/CreateDomain>`,
* :doc:`domain:update </EPPReference/CommandStructure/Update/UpdateDomain>`,
* :doc:`domain:renew </EPPReference/CommandStructure/RenewDomain>`,

and with responses to the
:doc:`domain:info </EPPReference/CommandStructure/Info/InfoDomain>` command.
