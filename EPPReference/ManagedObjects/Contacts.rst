
.. _mng-contact:

Contacts
--------

A contact contains information which represents a person or a company.

Namespace: \http://www.nic.cz/xml/epp/contact-1.6 |br|
Schema: contact-1.6.2.xsd

.. Note:: Contact mapping is based on the standard :rfc:`5733`
   but implemented with the following modifications:

   * addition of notification email, VAT-payer identification number, identity-document
     number and the type thereof,
   * replacement of two postal addresses with just one postal address.

.. _mng-contact-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, contacts also have
the following attributes:

``id``
   The contact handle. See :ref:`mngobj-handle-syntax`.

``postalInfo``
   Information for postal purposes, consisting of:

   ``name``
      The contact name (person or company).

   ``org``
      The name of an organization (use with a company). You may leave this empty
      to signify a natural person.

   ``addr``
      The permanent address / company seat, consisting of:

      ``street``
         1–3 street line(s).

      ``city``
         City.

      ``sp``
         State or province.

      ``pc``
         Postal code.

      ``cc``
         Country code.

``voice``
   Phone number.

``fax``
   Fax number.

``email``
   A list of email addresses.

``notifyEmail``
   A list of notification email addresses.

``vat``
   VAT-payer identifier.

``ident``
   Identity-document type and number. (A document that proves the contact's identity.)

``disclose``
   Disclosure preference for: ``addr``, ``voice``, ``fax``, ``email``, ``vat``,
   ``ident``, ``notifyEmail``.

   .. Note:: The contact handle, name and organization are always disclosed.

``mailing``/``addr`` :sup:`extension`
   An additional :ref:`mailing address <mng-contact-ext>`, which consists
   of the same items as the permanent address (``postalInfo``/``addr``).

.. _mng-contact-stat:

Object states
^^^^^^^^^^^^^^^^^

A contact can have one or more of the following statuses:

* ``ok`` – no other states are set
* ``linked`` – the contact has relation to other records in the Registry
* ``serverDeleteProhibited`` – deletion of the contact is forbidden
* ``serverTransferProhibited`` – transfer of the contact is forbidden
* ``serverUpdateProhibited`` – update of the contact is forbidden
* ``serverBlocked`` – the contact is blocked by administration
* ``deleteCandidate`` – the contact is scheduled for deletion
* ``conditionallyIdentifiedContact`` – the contact's identity is partially verified
* ``identifiedContact`` – the contact's identity is fully verified
* ``validatedContact`` – the contact is validated
* ``mojeidContact`` – the contact is used in the mojeID extension and has more
  attributes and possibilities than a regular contact

.. _mng-contact-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`contact:check </EPPReference/CommandStructure/Check/CheckContact>`
* :doc:`contact:create </EPPReference/CommandStructure/Create/CreateContact>`
* :doc:`contact:delete </EPPReference/CommandStructure/Delete/DeleteContact>`
* :doc:`contact:info </EPPReference/CommandStructure/Info/InfoContact>`
* :doc:`contact:transfer </EPPReference/CommandStructure/Transfer/TransferContact>`
* :doc:`contact:update </EPPReference/CommandStructure/Update/UpdateContact>`
* :doc:`contact:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoContact>`

.. top-level elements

   * command TLE: ``<contact:check>``, ``<contact:create>``, ``<contact:delete>``,
     ``<contact:info>``, ``<contact:transfer>``, ``<contact:update>``,
     ``<contact:sendAuthInfo>``

   * response data TLE: ``<contact:chkData>``, ``<contact:creData>``,
     ``<contact:infData>``

   * poll msg TLE: ``<contact:trnData>``, ``<contact:idleDelData>``,
     ``<contact:updateData>``

.. _mng-contact-ext:

Mailing address
^^^^^^^^^^^^^^^

:doc:`Command & response extensions </EPPReference/ProtocolBasics/ComResExtensions>`
allow to manage an additional address with a contact.

Namespace: \http://www.nic.cz/xml/epp/extra-addr-1.0 |br|
Schema: extra-addr-1.0.0.xsd

These extensions are used with the following commands:

* :doc:`contact:create </EPPReference/CommandStructure/Create/CreateContact>`,
* :doc:`contact:update </EPPReference/CommandStructure/Update/UpdateContact>`.

and with responses to the
:doc:`contact:info </EPPReference/CommandStructure/Info/InfoContact>` command.
