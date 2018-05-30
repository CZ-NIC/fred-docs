
.. _FRED-Admin-App-CSParams:

ClearSilver parameters reference
--------------------------------

This is a reference of available parameters which are passed to ClearSilver
templates when generating email based on events in the FRED.
See also `template syntax in ClearSilver <http://www.clearsilver.net/docs/man_templates.hdf>`_.

The parameters are listed for each email type and there is an index
with short descriptions of common parameters at the end of this appendix.

Email types can be found by their names in the table ``mail_type`` and
the templates for each type can be found in the table ``mail_template``.

.. contents:: Chapter TOC
   :local:
   :backlinks: none

.. _email-type-sendai-pif:

Email type: ``sendauthinfo_pif``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent in response to a request for a transfer password
  which was placed through the Registry website
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`authinfo <csparams-authinfo>`,
  :ref:`handle <csparams-handle>`,
  :ref:`reqdate <csparams-reqdate>`,
  :ref:`reqid <csparams-reqid>`,
  :ref:`type <csparams-type>`

.. _email-type-sendai-epp:

Email type: ``sendauthinfo_epp``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent in response to a request for a transfer password
  which was placed through a registrar
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`authinfo <csparams-authinfo>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`type <csparams-type>`

.. _email-type-expired-notify:

Email type: ``expiration_notify``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the domain owner in response to the domain expiration
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`administrators <csparams-administrators>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`owner <csparams-owner>`,
  :ref:`registrar <csparams-registrar>`,

.. _email-type-expired-outzone-warning-own:

Email type: ``expiration_dns_warning_owner``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the domain owner in response to the upcoming exclusion of a domain
  from the zone
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`administrators <csparams-administrators>`,
  :ref:`day_before_exregdate <csparams-day_before_exregdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`owner <csparams-owner>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`zone <csparams-zone>`

.. _email-type-expired-outzone-own:

Email type: ``expiration_dns_owner``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the domain owner in response to the exclusion of a domain from the zone
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`administrators <csparams-administrators>`,
  :ref:`day_before_exregdate <csparams-day_before_exregdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`owner <csparams-owner>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`zone <csparams-zone>`

.. _email-type-expired-delwarn-own:

Email type: ``expiration_register_owner``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the domain owner in response to the upcoming domain cancellation
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`domain <csparams-domain>`,

.. _email-type-expired-outzone-tech:

Email type: ``expiration_dns_tech``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the technical contacts of the nsset whose domain was just excluded
  from zone
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`domain <csparams-domain>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`statechangedate <csparams-statechangedate>`

.. _email-type-expired-deleted-tech:

Email type: ``expiration_register_tech``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the technical contacts of the nsset whose domain was just cancelled
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`domain <csparams-domain>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`nsset <csparams-nsset>`,

.. _email-type-valid-warn:

Email type: ``expiration_validation_before``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the owner of an ENUM domain in response to the upcoming expiry
  of domain's validation
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`administrators <csparams-administrators>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`valdate <csparams-valdate>`

.. _email-type-valid:

Email type: ``expiration_validation``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the owner of the ENUM domain in response to the expiry
  of domain's validation
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`administrators <csparams-administrators>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`registrar <csparams-registrar>`,

.. _email-type-notify-create:

Email type: ``notification_create``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent when a new object (domain, contact, nsset, keyset) is created,
  to the email contact of the created object
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`ticket <csparams-ticket>`,
  :ref:`type <csparams-type>`

* additional parameters concerning a new **contact**:
   * ``fresh.object.authinfo`` – transfer password
   * ``fresh.contact.name`` – name of contact person
   * ``fresh.contact.org`` – organization name
   * ``fresh.contact.address.permanent`` – permanent personal address
     / organization headquarters address
   * ``fresh.contact.address.mailing`` – mailing address
   * ``fresh.contact.address.billing`` – billing address
   * ``fresh.contact.address.shipping`` – 1\ :sup:`st` shipping address
   * ``fresh.contact.address.shipping_2`` – 2\ :sup:`nd` shipping address
   * ``fresh.contact.address.shipping_3`` – 3\ :sup:`rd` shipping address
   * ``fresh.contact.telephone`` – phone/mobile number
   * ``fresh.contact.fax`` – fax number
   * ``fresh.contact.email`` – email address
   * ``fresh.contact.notify_email`` – notification email address
   * ``fresh.contact.ident_type`` – type of personal identification
   * ``fresh.contact.ident`` – personal identifier
   * ``fresh.contact.vat`` – VAT-payer registration number (DIČ)
   * ``fresh.contact.disclose.name`` – name disclosure setting (show/hide)
   * ``fresh.contact.disclose.org`` – organization disclosure setting (show/hide)
   * ``fresh.contact.disclose.email`` – email disclosure setting (show/hide)
   * ``fresh.contact.disclose.address`` – address disclosure setting (show/hide)
   * ``fresh.contact.disclose.notify_email`` – notification email disclosure
     setting (show/hide)
   * ``fresh.contact.disclose.ident`` – personal identifier disclosure setting
     (show/hide)
   * ``fresh.contact.disclose.vat`` – VAT-payer identification number disclosure
     setting (show/hide)
   * ``fresh.contact.disclose.telephone`` – phone number disclosure setting
     (show/hide)
   * ``fresh.contact.disclose.fax`` – fax number disclosure setting (show/hide)

* There are no additional parameters concerning new objects of other types
  (domain, nsset, keyset).

.. _email-type-notify-update:

Email type: ``notification_update``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent after an object (domain, contact, nsset, keyset)
  is updated, to the email contact of the updated object
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`ticket <csparams-ticket>`,
  :ref:`type <csparams-type>`

* additional parameters concerning changes in an object:

   * ``changes`` – general indication of changes: ``0`` – there are **no**
     changes, ``1`` – there are some changes
   * Whether a change has occured or not, is indicated for each attribute
     of an object and parameters containing both the old and the new
     value of the attribute are passed in the following manner:

      * :samp:`changes.{<object>}.{<attribute>}` indicates a change in an attribute
        – if the attribute has changed, it contains the value ``1``;
        otherwise the parameter is not passed,
      * :samp:`changes.{<object>}.{<attribute>}.old` contains the value of the attribute
        before the change (passed only if the attribute has changed),
      * :samp:`changes.{<object>}.{<attribute>}.new` contains the value of the attribute
        after the change (passed only if the attribute has changed).

   * :samp:`changes.object.authinfo` – indicates that the object's transfer
     password has changed,
   * Indication of changes of other attributes is specific for each object type
     as follows.

* additional parameters concerning changes in a **contact**:
   * ``changes.contact.name`` – contact name has changed
   * ``changes.contact.org`` – organization name has changed
   * ``changes.contact.telephone`` – phone number has changed
   * ``changes.contact.fax`` – fax number has changed
   * ``changes.contact.email`` – email address has changed
   * ``changes.contact.notify_email`` – notification email address has changed
   * ``changes.contact.ident_type`` – type of personal identification has
     changed
   * ``changes.contact.ident`` – personal identifier has changed
   * ``changes.contact.vat`` – VAT-payer registration number (DIČ) has changed
   * ``changes.contact.address.permanent`` – permanent (headquarters) address
     has changed
   * ``changes.contact.address.mailing`` – mailing address has changed
   * ``changes.contact.address.billing`` – billing address has changed
   * ``changes.contact.address.shipping`` – 1\ :sup:`st` shipping address
     has changed
   * ``changes.contact.address.shipping_2`` – 2\ :sup:`nd` shipping address
     has changed
   * ``changes.contact.address.shipping_3`` – 3\ :sup:`rd` shipping address
     has changed
   * ``changes.contact.disclose.name`` – name disclosure setting has changed
   * ``changes.contact.disclose.org`` – organization disclosure setting has
     changed
   * ``changes.contact.disclose.email`` – email disclosure setting has changed
   * ``changes.contact.disclose.address`` – address disclosure setting has
     changed
   * ``changes.contact.disclose.notify_email`` – notification email disclosure
     setting has changed
   * ``changes.contact.disclose.ident`` – personal identifier disclosure
     setting has changed
   * ``changes.contact.disclose.vat`` – VAT-payer number disclosure setting
     has changed
   * ``changes.contact.disclose.telephone`` – phone number disclosure setting
     has changed
   * ``changes.contact.disclose.fax`` – fax number disclosure setting has
     changed
* additional parameters concerning changes in a **nsset**:
   * ``changes.nsset.check_level`` – level of technical checks has changed
   * ``changes.nsset.tech_c`` – list of technical contacts has changed
   * ``changes.nsset.dns`` – list of name servers has changed
      * the old and new value of each name server can be accessed using
        an index number (counting from zero) at the end of the parameter name,
        for example:
      * ``changes.nsset.dns.old.1`` – the value of the second name server
        before the change,
      * ``changes.nsset.dns.new.1`` – the value of the second name server
        after the change.
* additional parameters concerning changes in a **domain**:
   * ``changes.domain.registrant`` – domain owner has changed
   * ``changes.domain.nsset`` – nsset assignment has changed
   * ``changes.domain.keyset`` – keyset assignment has changed
   * ``changes.domain.admin_c`` – list of administrative contacts has changed
   * ``changes.domain.temp_c`` :sup:`DEPRECATED` – list of temporary contacts has changed
   * ``changes.domain.val_ex_date`` :sup:`ENUM` – date of validation expiry
     has changed
   * ``changes.domain.publish`` :sup:`ENUM` – publication in telephone
     directory has changed
* additional parameters concerning changes in a **keyset**:
   * ``changes.keyset.tech_c`` – list of technical contacts has changed
   * ``changes.keyset.dnskey`` – list of DNS keys has changed

.. _email-type-notify-transfer:

Email type: ``notification_transfer``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent after an object (domain, contact, nsset, keyset) is transferred
  to a new registrar, to the email contact of the transferred object
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`ticket <csparams-ticket>`,
  :ref:`type <csparams-type>`

.. _email-type-notify-renew:

Email type: ``notification_renew``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent after a domain is renewed, to its owner's email
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`ticket <csparams-ticket>`,
  :ref:`type <csparams-type>`

.. _email-type-notify-idle:

Email type: ``notification_unused``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent after an unused object (contact, keyset, nsset) is removed
  from the database, to the email contact of the removed object
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`deldate <csparams-deldate>`,
  :ref:`handle <csparams-handle>`,
  :ref:`type <csparams-type>`

.. _email-type-notify-delete:

Email type: ``notification_delete``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent after an object (domain, contact, nsset, keyset) is deleted,
  to the email contact of the deleted object
* passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`ticket <csparams-ticket>`,
  :ref:`type <csparams-type>`

.. _email-type-techcheck:

Email type: ``techcheck``
^^^^^^^^^^^^^^^^^^^^^^^^^

* sent if a test in a :doc:`technical check </Concepts/Teccheck>` of a nsset
  has failed, as a report to technical contacts of the nsset
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`registrar <csparams-registrar>`

* additional parameters:
   * ``checkdate`` – date on which the technical check was performed
   * ``ticket`` – check number
   * ``tests`` – list of datasets with results of the tests which
     have failed; a single dataset (one list item, e.g. ``tests.0``) has the
     following attributes:

      * :samp:`tests.*.type` – severity of the test result (\ ``error`` / ``warning`` / ``notice``),
      * :samp:`tests.*.name` – subject of the test,
      * :samp:`tests.*.ns` – further information about the test result
        whose content depends on the test subject.

     The content of further information about the result according to the test subject
     (value of the ``name`` attribute):

      * ``glue_ok`` – the required glue record is missing for the following name servers:
         - :samp:`tests.*.ns` – list of the name servers,
      * ``existence`` – following name servers in the nsset are unreachable:
         - :samp:`tests.*.ns` – list of the name servers,
      * ``autonomous`` – the nsset does not contain at least two name servers in different autonomous systems:
         - no more content,
      * ``presence`` – name server(s) exists which does not contain a record for any of the domains:
         - :samp:`tests.*.ns` – list of the name servers,
         - :samp:`tests.*.ns.*.fqdn` – list of the domains for a particular
           name server of which this name server does not contain a record,
         - :samp:`tests.*.ns.overfull` – the list of domains is incomplete /
           there are more domains in the test input for which this name server
           does not contain a record but they are not all listed (this
           can be used to insert an ellipsis  - ..." conditionally),
      * ``authoritative`` – name server is not authoritative for domains:
         - :samp:`tests.*.ns` – list of the name servers,
         - :samp:`tests.*.ns.*.fqdn` – list of the domains for a particular
           name server of which this name server is not authoritative,
         - :samp:`tests.*.ns.overfull` – the list of domains is incomplete /
           there are more domains in the test input for which this name server
           is not authoritative but they are not all listed (this
           can be used to insert an ellipsis "..." conditionally),
      * ``heterogenous`` – all name servers in the nsset use the same implementation of dns server:
         - no more content,
      * ``notrecursive`` – following name servers in the nsset are recursive:
         - :samp:`tests.*.ns` – list of the name servers,
      * ``notrecursive4all`` – following name servers in the nsset answered a query recursively:
         - :samp:`tests.*.ns` – list of the name servers,
      * ``dnsseckeychase`` – for the following domains belonging to the nsset, the validity of the dnssec signature could not be verified:
         - :samp:`tests.*.ns` – list of the domains.

     The original template defines and uses the ``printtest()`` macro which accepts
     a result dataset (an item from the ``tests`` list) as an argument and
     prints the results according to the subject (\ ``name``) of the test. Print
     of the test results is grouped by severity.

.. _email-type-request-block:

Email type: ``request_block``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the domain owner / the contact / technical contacts of an object
  after a :term:`public request` for object (un)blocking has been carried out
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`,
  :ref:`reqdate <csparams-reqdate>`,
  :ref:`reqid <csparams-reqid>`,
  :ref:`type <csparams-type>`
* additional parameters:
   * ``otype`` – operation type: ``1`` – blocking, ``2`` – unblocking,
   * ``rtype`` – request type: ``1`` – all object changes, ``2`` – object transfer.

.. _email-type-contact-reminder:

Email type: ``annual_contact_reminder``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to a contact in response to the upcoming contact registration anniversary
  as a reminder to check accuracy of contact information in the registry
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`
* additional parameters:
   * ``organization`` – name of contact's organization,
   * ``name`` – personal or company name,
   * ``address`` – address (in a single line),
   * ``ident_type`` – identity-document identification type:
      * ``RC`` – birth number,
      * ``OP`` – personal ID card number,
      * ``PASS`` – passport number,
      * ``ICO`` – organization ID number,
      * ``MPSV`` – MPSV ID (number from the Ministry of Labour and Social Affairs),
      * ``BIRTHDAY`` – the date of birth,
   * ``ident_value`` – identity-document identification number,
   * ``dic`` – VAT-payer identifier,
   * ``telephone`` – phone number,
   * ``fax`` – fax number,
   * ``email`` – email address,
   * ``notify_email`` – notification email address,
   * ``registrar_name`` – name of the :term:`designated registrar`,
   * ``registrar_url`` – website address of the :term:`designated registrar`,
   * ``registrar_memo_cz`` – a memo provided by the registrar (Czech/local variant),
   * ``registrar_memo_en`` – a memo provided by the registrar (English variant),

     .. Note:: The registrar memo is :ref:`configurable <config-contact-reminder>`.

   * ``domains`` – list of domains where the contact is the owner,
   * ``nssets`` – list of nssets where the contact is a technical contact,
   * ``keysets`` – list of keysets where the contact is a technical contact.

.. _email-type-merged-contact:

Email type: ``merge_contacts_auto``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent to the contact after an automatic merger of its duplicates
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`
* additional parameters:
   * ``dst_contact_handle`` – handle of the destination contact into which the
     duplicates have been merged,
   * ``domain_registrant_list`` – list of handles of domains in which the
     registrant contact had to be replaced with the destination contact,
   * ``domain_admin_list`` – list of handles of domains in which some
     administrative contacts had to be replaced with the destination contact,
   * ``nsset_tech_list`` – list of handles of nssets in which some technical
     contacts had to be replaced with the destination contact,
   * ``keyset_tech_list`` – list of handles of keysets in which some technical
     contacts had to be replaced with the destination contact,
   * ``removed_list`` – list of contacts which have been deleted as a result
     of the merger.

  Values of the lists can be accessed by adding an index number at the end
  of the parameter name, counting from zero, for example: ``domain_registrant_list.0``
  for the first item.

.. _email-type-akm-ok:

Email type: ``akm_candidate_state_ok``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent after valid CDNSKEY records are discovered on a insecured domain
  and the acceptance period is initiated,
  to technical contacts of the domain's nsset
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`domain <csparams-domain>`,
  :ref:`zone <csparams-zone>`

* additional parameters:

   * ``keys`` – list of discovered CDNSKEY records (the first item of the list as ``keys.0`` etc.),
     a single key item looks like this::

        [flags: 257, protocol: 3, algorithm: 13, key: "mdsswUyr3DPW132mOi8V9xESWE8jTo0dxCjjnopKl+GqJxpVXckHAeF+KkxLbxILfDLUT0rAK9iUzy1L53eKGQ=="]

   * ``datetime`` – date and time of the discovery,

   * ``days_to_left`` – how many days the acceptance period is going to last.

.. _email-type-akm-ko:

Email type: ``akm_candidate_state_ko``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent when the acceptance period is broken by absence of the CDNSKEY records
  or by discovery of changed records, to technical contacts of the domain's nsset
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`
  :ref:`domain <csparams-domain>`
* additional parameters:
   * ``datetime`` – date and time of the discovery.

.. _email-type-akm-upd:

Email type: ``akm_keyset_update``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent when an auto-managed keyset is updated from new CDNSKEY records,
  to technical contacts of the domain's nsset
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
  :ref:`domain <csparams-domain>`,
  :ref:`zone <csparams-zone>`
* additional parameters:
   * ``keys`` – list of discovered CDNSKEY records (the first item of the list
     as ``keys.0`` etc.),
   * ``datetime`` – date and time of the discovery.

.. _email-type-rs:

Email type: ``record_statement``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent in response to a request for a registry record statement about an object,
  to the email of the domain owner / the contact / technical contacts
* common passed parameters:
  :ref:`defaults.* <csparams-defaults>`,
* additional parameters:
   * ``request_day`` – the day of the request date,
   * ``request_month`` – the month of the request date,
   * ``request_year`` – the year of the request date.

.. _email-type-personal-info:

Email type: ``sendpersonalinfo_pif``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* sent in response to a resolved :term:`public request` for personal information
  of a contact, to the email selected within the request
* common passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`handle <csparams-handle>`
* additional parameters:
   * ``name`` – name (personal),
   * ``organization`` – name of an organization,
   * ``address`` – main (permanent) address,
   * ``mailing_address`` – mailing address,
   * ``billing_address`` – billing address,
   * ``shipping_address_1`` – 1\ :sup:`st` shipping address,
   * ``shipping_address_2`` – 2\ :sup:`nd` shipping address,
   * ``shipping_address_3`` – 3\ :sup:`rd` shipping address,
   * ``ident_type`` – identity document type,
   * ``ident_value`` – identity document number,
   * ``dic`` – :term:`VAT`-payer number,
   * ``telephone`` – phone number,
   * ``fax`` – fax number,
   * ``email`` – main email address,
   * ``notify_email`` – notification email address,
   * ``registrar_name`` – name of the designated registrar,
   * ``registrar_url`` – website of the designated registrar.

.. _csparams-description:

Description of parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

This section contains description of parameters which are common to several
email types.

.. _csparams-defaults:

Registry information (defaults)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These parameters are passed to all email types and can be found and adapted
in the table ``mail_defaults``.

* ``defaults.company`` – name of the Registry
* ``defaults.street`` – street in the headquarters address of the Registry
* ``defaults.postalcode`` – postal code in the headquarters address of the
  Registry
* ``defaults.city`` – city in the headquarters address of the Registry
* ``defaults.tel`` – phone contact of the Registry
* ``defaults.fax`` – fax contact of the Registry
* ``defaults.emailsupport`` – email contact of the technical support
* ``defaults.authinfopage`` – URL of the site from which registrants can
  request the transfer password (authinfo)
* ``defaults.whoispage`` – URL of the site from which the public can search
  in the Registry
* ``defaults.company_cs`` – Czech variant of the company name of the Registry
* ``defaults.company_en`` – English variant of the company name of the Registry

Common parameters
~~~~~~~~~~~~~~~~~

   .. _csparams-administrators:

   ``administrators``
      list of administrative contacts (items are accessed by adding index
      number at the end of the parameter name, counting from zero,
      for example: ``administrators.0`` for the first item)

   .. _csparams-authinfo:

   ``authinfo``
      transfer password

   .. _csparams-checkdate:

   ``checkdate``
      the date when the object-state check was performed and this email created
      (according to the server's local time, date format: YYYY-MM-DD)

   .. _csparams-deldate:

   ``deldate``
      date of deletion of an idle (obsolete) object

   .. _csparams-dnsdate:

   ``dnsdate``
      date from which the domain will not be included in the zone anymore

   .. _csparams-domain:

   ``domain``
      domain name in question

   .. _csparams-exdate:

   ``exdate``
      date of domain expiration (till when the registration has been prepaid)

   .. _csparams-exregdate:

   ``exregdate``
      date from which the domain can be registered by another subject
      (domain is unguarded)

   .. _csparams-day_before_exregdate:

   ``day_before_exregdate``
      date of the last day the domain is guarded
      (one day before registration cancellation)

   .. _csparams-handle:

   ``handle``
      string identifier of the object in question

   .. _csparams-owner:

   ``owner``
      identifier of the owner of the domain in question (contact handle)

   .. _csparams-nsset:

   ``nsset``
      identifier of the name server set assigned to the domain in question
      (nsset handle)

   .. _csparams-registrar:

   ``registrar``
      name and website of the current designated registrar
      (in case of transfer, the new designated registrar)

   .. _csparams-reqdate:

   ``reqdate``
      the date when the public request was placed (date format dd.mm.YYYY)

   .. _csparams-reqid:

   ``reqid``
      the identification number of the public request by which it can be traced
      in the Registry

   .. _csparams-statechangedate:

   ``statechangedate``
      date when the respective object state was set

   .. _csparams-ticket:

   ``ticket``
      email identifier

   .. _csparams-type:

   ``type``
      object type by number: ``1`` – contact, ``2`` – nsset, ``3`` – domain,
      ``4`` – keyset

   .. _csparams-valdate:

   ``valdate``
      date till when the ENUM domain has been validated

   .. _csparams-zone:

   ``zone``
      zone in question (FQDN with the leading dot)
