
.. _mng-contact:

Contacts
--------

Contact information of a person or a company.

Namespace: \http://www.nic.cz/xml/epp/contact-1.6 |br|
Schema: contact-1.6.2.xsd

..
   todo:: https://tools.ietf.org/html/rfc5733#section-2

.. _mng-contact-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, contacts also have
the following attributes:

id
   The contact handle. See :ref:`mngobj-handle-syntax`.

postalInfo
   Information for the purpose of ordinary mailing, consisting of:

   name
      The contact name. (personal or company)

   org
      The name of an organization.

   addr
      The real-world contact address, consisting of:

      street
         Street line.

      city
         City.

      sp
         State or province.

      pc
         Postal code.

      cc
         Country code.

voice
   Phone number.

fax
   Fax number.

email
   Email address(es).

notifyEmail
   Notification email address(es).

vat
   VAT-payer identifier.

ident
   Identity-document type and number. (A document that proves the contact's identity.)

disclose
   Disclosure preference for: addr, voice, fax, email, vat, ident, notifyEmail.

   .. Note:: The contact handle, name and organization are always disclosed.

.. top-level elements

   * command TLE: ``<contact:check>``, ``<contact:create>``, ``<contact:delete>``,
     ``<contact:info>``, ``<contact:transfer>``, ``<contact:update>``,
     ``<contact:sendAuthInfo>``

   * response data TLE: ``<contact:chkData>``, ``<contact:creData>``,
     ``<contact:infData>``

   * poll msg TLE: ``<contact:trnData>``, ``<contact:idleDelData>``,
     ``<contact:updateData>``

.. _mng-contact-stat:

Object states
^^^^^^^^^^^^^^^^^

A contact can have one or more of the following statuses:

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
  attributes and possibilities than a regular contact

.. _mng-contact-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`contact:check </EPPReference/CommandStructure/Check/CheckContact>`
* :doc:`contact:create </EPPReference/CommandStructure/Create/CreateContact>`
* :doc:`contact:delete </EPPReference/CommandStructure/Delete/DeleteContact>`
* :doc:`contact:info </EPPReference/CommandStructure/Info/InfoContact>`
* :doc:`contact:transfer </EPPReference/CommandStructure/Transfer/TransferContact>`
* :doc:`contact:update </EPPReference/CommandStructure/Update/UpdateContact>`
* :doc:`contact:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoContact>`
