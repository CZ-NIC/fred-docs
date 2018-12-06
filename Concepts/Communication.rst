


Communication
=============

This chapter provides an overview of communication which is triggered by events
in the Registry.

.. contents:: Chapter TOC
   :local:
   :backlinks: none

.. _comm-channels:

Channels
--------

The FRED is capable of using the following channels of communication:

* Email
   * mandatory in contacts and registrars
   * used for most communication
* Notify email
   * optional, contacts only
   * used for notifications only
   * If a contact does not have a notify email, it is not notified.
* Generic and additional emails
   * extra addresses unrelated to registry records
   * used only for `outzone unguarded warnings`_ (life-cycle event)
* Poll messages
   * an integral part of EPP
   * used for communication with registrars related to EPP activity
* Letter :term:`CZ-specific`
* Registered letter :term:`CZ-specific`
* SMS :term:`CZ-specific`

.. _comm-channels-generic:

Generic email addresses :sup:`CZ-specific`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The generic email addresses are a qualified guess in an attempt to reach
domain stakeholders. The Registry applies a set of patterns with `local-part
<https://en.wikipedia.org/wiki/Email_address>`_ names
which the stakeholders often use to name their domain-based mailboxes.

The generic email addresses are generated based on the following patterns:
\ ``info@<fqdn>``, ``kontakt@<fqdn>``, ``postmaster@<fqdn>``,
\ ``<fqdn>@<fqdn>`` where ``<fqdn>`` is the domain name in question.

The patterns for the generic email addresses are hard-coded.

.. _comm-objmodif:

Object modifications
--------------------

This section describes communication that arises from modifications
of :term:`registrable object`\ s by registrars, **except** the system registrar.

Modifications must finish successfully for notifications to occur.

.. list-table::
   :name: Object modifications
   :header-rows: 1
   :stub-columns: 1
   :widths: 20, 30, 30, 20

   * - Name
     - Trigger
     - Addressee
     - Channel
   * - Create notification
     -
     -
     - Notify email |br|
       (:ref:`CS params <email-type-notify-create>`)
   * -
     - Registrar created a domain
     - :ref:`Holder and admin. contacts <contact-roles>`
     -
   * -
     - Registrar created a contact
     - The contact
     -
   * -
     - Registrar created an nsset
     - :ref:`Tech. contacts <contact-roles>`
     -
   * -
     - Registrar created a keyset
     - :ref:`Tech. contacts <contact-roles>`
     -
   * -
     -
     -
     -
   * - Delete notification
     -
     -
     - Notify email |br|
       (:ref:`CS params <email-type-notify-delete>`)
   * -
     - Registrar deleted a domain
     - :ref:`Holder and admin. contacts <contact-roles>`
     -
   * -
     - Registrar deleted a contact
     - The contact
     -
   * -
     - Registrar deleted an nsset
     - :ref:`Tech. contacts <contact-roles>`
     -
   * -
     - Registrar deleted a keyset
     - :ref:`Tech. contacts <contact-roles>`
     -
   * -
     -
     -
     -
   * - Renew notification
     - Registrar renewed a domain
     - :ref:`Holder and admin. contacts <contact-roles>`
     - Notify email |br|
       (:ref:`CS params <email-type-notify-renew>`)
   * -
     -
     -
     -
   * - Transfer notification
     -
     -
     - Notify email |br|
       (:ref:`CS params <email-type-notify-transfer>`)
   * -
     - Registrar transferred a domain
     - :ref:`Holder and admin. contacts <contact-roles>`
     -
   * -
     - Registrar transferred a contact
     - The contact
     -
   * -
     - Registrar transferred an nsset
     - :ref:`Tech. contacts <contact-roles>`
     -
   * -
     - Registrar transferred a keyset
     - :ref:`Tech. contacts <contact-roles>`
     -
   * -
     - Registrar transferred an object
     - Previous registrar
     - Poll message (:ref:`structure <epp-poll-type-transfer>`)
   * -
     -
     -
     -
   * - Update notification
     -
     -
     - Notify email |br|
       (:ref:`CS params <email-type-notify-update>`)
   * -
     - Registrar updated a domain
     - :ref:`Holder and admin. contacts <contact-roles>` |br|
       both old and new
     -
   * -
     - Registrar updated a contact
     - The contact |br|
       both old and new notify email
     -
   * -
     - Registrar updated an nsset
     - :ref:`Tech. contacts <contact-roles>` |br|
       both old and new
     -
   * -
     - Registrar updated a keyset
     - :ref:`Tech. contacts <contact-roles>` |br|
       both old and new
     -



Settings
^^^^^^^^

Configuration allows to disable all EPP notifications in the Registry altogether
(allowed by default):

.. code-block:: ini
   :caption: Configure in the **fred-rifd** configuration file

   [registry]
   disable_epp_notifier = true

It is also possible to allow registrars to disable EPP notifications per command
by configuring a special prefix for client transaction identifiers:

.. code-block:: ini
   :caption: Configure in the **fred-rifd** configuration file

   [registry]
   disable_epp_notifier_cltrid_prefix = no_notification_

When the registrar signs a command with a client transaction identifier
starting with the prefix ``no_notification_``, the operation will not trigger
a notification.

.. _comm-objlife:

Life-cycle events
-------------------

This section describes communication that arises from the :doc:`life cycle of
registrable objects </Concepts/LifeCycle/index>` (state changes).

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 20, 30, 30, 20

   * - Name
     - Trigger
     - Addressee
     - Channel
   * - Expiration warning
     - Domain expiration is approaching – the :ref:`expW state <registration-expiration>`
       has been reached
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-domain-exp>`)
   * - Expiration notice
     - Domain has :ref:`expired <registration-expiration>`
     - :ref:`Holder and admin. contacts <contact-roles>`
     - Email (:ref:`CS params <email-type-expired-notify>`)
   * -
     -
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-domain-exp>`)
   * - Outzone warning (unguarded)
     - Domain is becoming unguarded – the :ref:`ouW state <registration-expiration>`
       has been reached
     - :ref:`Generics + additionals <comm-channels-generic>`
     - Email (:ref:`CS params <email-type-expired-outzone-warning-own>`)
   * - Outzone notice (unguarded)
     - Domain has become :ref:`unguarded <registration-expiration>`
     - :ref:`Holder and admin. contacts <contact-roles>`
     - Email (:ref:`CS params <email-type-expired-outzone-own>`)
   * -
     -
     - :ref:`Technical contacts <contact-roles>` of the domain's nsset
     - Email (:ref:`CS params <email-type-expired-outzone-tech>`)
   * -
     -
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-domain-exp>`)
   * - Deletion warning |br| :term:`CZ-specific`
     - Domain is going to be deleted – the :ref:`delW state <registration-expiration>`
       has been reached
     - :ref:`Holder <contact-roles>`
     - Letter
   * - Deletion notice
     - Domain is being deleted – the
       :ref:`deleteCandidate state <registration-expiration>` has been reached
     - :ref:`Holder and admin. contacts <contact-roles>`
     - Email (:ref:`CS params <email-type-expired-delwarn-own>`)
   * -
     -
     - :ref:`Technical contacts <contact-roles>` of the domain's nsset
     - Email (:ref:`CS params <email-type-expired-deleted-tech>`)
   * -
     -
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-domain-exp>`)
   * - 1\ :sup:`st` validation warning
     - Validation of an ENUM domain is expiring – the :ref:`valW1 state
       <validation-expiration>` has been reached
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-domain-val>`)
   * - 2\ :sup:`nd` validation warning
     - Validation of an ENUM domain is expiring – the :ref:`valW2 state
       <validation-expiration>` has been reached
     - :ref:`Holder and admin. contacts <contact-roles>` of the domain
     - Email (:ref:`CS params <email-type-valid-warn>`)
   * - Outzone notice (not validated)
     - Validation of an ENUM domain has expired – the domain is :ref:`not validated
       <validation-expiration>` anymore
     - :ref:`Holder, admin. contacts and tech. contacts of the nsset <contact-roles>`
     - Email (:ref:`CS params <email-type-valid>`)
   * -
     -
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-domain-val>`)
   * - Unused notification
     - Object (nsset, keyset, or contact) has become :doc:`obsolete
       </Concepts/LifeCycle/NonDomains>` and is being deleted
     - :ref:`Technical contacts <contact-roles>` or the contact
     - Notify email (:ref:`CS params <email-type-notify-idle>`)


Outzone unguarded warnings
^^^^^^^^^^^^^^^^^^^^^^^^^^

These warnings are sent to :ref:`generic <comm-channels-generic>` and additional
custom email addresses which are not direcly related to records in the Registry
database.

Additional email addresses can be manually loaded to the Registry in the WebAdmin
(Daphne). You just import a CSV file with domain names and lists of email addresses
to send the warning email to.

.. code-block:: none
   :caption: Example of a line in a CSV file with additional emails

   domain.tld,mail@example.tld,anothermail@example.tld,etc@example.tld

After the warnings are sent, the list of additional email addresses is cleared
in the Registry database. A new list of addresses must be imported if there is
need for another warning of this type.

Settings
^^^^^^^^

To disable these messages, remove the corresponding row in the database table
``notify_statechange_map`` for the state change you do not wish to communicate.

To modify when the messages are sent, reconfigure parameters of the :doc:`life cycle
</Concepts/LifeCycle/index>` itself.

.. _comm-admin:

Administrative events
---------------------

This section describes communication that arises from administrative tasks of the Registry.

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 20, 30, 30, 20

   * - Name
     - Trigger
     - Addressee
     - Channel
   * - Contact merger
     - Registry has merged a contact automatically because it was detected as a duplicate
     - The contact
     - Email (:ref:`CS params <email-type-merged-contact>`)
   * - Object update (contact merger)
     - Registry has updated an object as a result of contact merger
       (replaced duplicate contacts in linked objects)
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-update>`)
   * - Contact update (address disclosure)
     - Registry has changed disclosure of contact address
       (contact has started or stopped complying with the
       :ref:`rules for hiding address <epp-rules-hiding-address>`)
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-update>`)
   * - Contact reminder
     - Contact registration anniversary is approaching in 2 months
     - The contact
     - Email (:ref:`CS params <email-type-contact-reminder>`)
   * - Domain update (Admin.blocking)
     - Registry has updated a domain
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-update>`)
   * - Domain delete (Admin.verification)
     - Registry has deleted a domain
     - Registrar
     - Poll message
   * - Tech.check results
     - Registry has carried out a check requested by a registrar
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-techcheck>`)
   * - Tech.check results
     - Registry has carried out a periodic check, which has failed
     - :ref:`Technical contacts <contact-roles>` of the nsset
     - Email (:ref:`CS params <email-type-techcheck>`)
   * - :doc:`/Concepts/AKM` – Acceptance period iniated
     - Registry has discovered valid CDNSKEY records on an insecured domain
     - :ref:`Technical contacts <contact-roles>` of the nsset
     - Email
   * - :doc:`/Concepts/AKM` – Acceptance period broken
     - Registry has detected that CDNSKEY records changed during the acceptance period
     - :ref:`Technical contacts <contact-roles>` of the nsset
     - Email
   * - :doc:`/Concepts/AKM` – Acceptance period completed
     - Registry has updated a domain with the newly accepted key set
     - See :ref:`Update notification <Object modifications>`
     -
   * -
     -
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-update>`)
   * - :doc:`/Concepts/AKM` – Keys update
     - Registry has discovered new valid CDNSKEY records on a secured domain
     - :ref:`Technical contacts <contact-roles>` of the nsset
     - Email (:ref:`CS params <email-type-akm-upd>`)

.. _comm-requests:

Public request events
---------------------

This section describes communication that arises from requests of the public
submitted through a web form.

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 20, 30, 30, 20

   * - Name
     - Trigger
     - Addressee
     - Channel
   * - Authinfo
     - Request for authinfo, which has been placed as a :term:`public request`
     - :ref:`Linked contacts <contact-roles>` or the contact
     - Email (:ref:`CS params <email-type-sendai-pif>`)
   * - Authinfo
     - Request for authinfo, which has been placed through a registrar
     - :ref:`Linked contacts <contact-roles>` or the contact
     - Email (:ref:`CS params <email-type-sendai-epp>`)
   * - Blocking confirmation
     - Public request for object (un)blocking has been executed
     - :ref:`Linked contacts <contact-roles>` or the contact
     - Email (:ref:`CS params <email-type-request-block>`)
   * - Personal information
     - Request for personal information, which has been placed
       as a :term:`public request`
     - The contact
     - Email (:ref:`CS params <email-type-personal-info>`)

.. unimplemented in a front end
   * - Record statement
     - Request for record statement, which has been placed through webwhois
     - :ref:`Linked contacts <contact-roles>` or the contact
     - Email (:ref:`CS params <email-type-rs>`)

.. _comm-registrars:

Registrar events
----------------

This section describes communication that arises from registrar administration.

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 20, 30, 30, 20

   * - Name
     - Trigger
     - Addressee
     - Channel
   * - Low credit
     - Registrar's credit has dropped below :ref:`the limit <comm-registrars-settings>`
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-low-credit>`)
   * - Request usage
     - Daily (depends on the :ref:`task setup <cronjob-registrars-usage>`)
     - Registrar
     - Poll message (:ref:`structure <epp-poll-type-request-usage>`)
   * - Monthly bill – No audit invoice |br| :term:`CZ-specific`
     - The end of the month in which paid services were not used
     - Registrar
     - Email
   * - Monthly bill – Audit invoice included |br| :term:`CZ-specific`
     - The end of the month in which paid services were used
     - Registrar
     - Email
   * - Confirmation of a received payment for credit deposit – Advance invoice included |br| :term:`CZ-specific`
     - An advance payment has been matched
     - Registrar
     - Email

.. _comm-registrars-settings:

Settings
^^^^^^^^

The credit limit for the *low credit* message can be configured per zone
in the database table ``poll_credit_zone_limit``.
