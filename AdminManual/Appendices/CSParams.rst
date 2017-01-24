
.. _FRED-Admin-App-CSParams:

Appendix: ClearSilver parameters reference
------------------------------------------

This is a reference of available parameters which are passed to ClearSilver
templates when generating email based on events in the FRED.
The parameters are listed for each email type and there is an index
with short descriptions of common parameters at the end of this appendix.


Email type: ``sendauthinfo_pif``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent in response to a request for a transfer password
  which was placed through the Registry website
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`registrar <csparams-registrar>`, :ref:`reqdate <csparams-reqdate>`,
  :ref:`reqid <csparams-reqid>`, :ref:`type <csparams-type>`,
  :ref:`handle <csparams-handle>`, :ref:`authinfo <csparams-authinfo>`

Email type: ``sendauthinfo_epp``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent in response to a request for a transfer password
  which was placed through a registrar
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`registrar <csparams-registrar>`, :ref:`reqdate <csparams-reqdate>`,
  :ref:`reqid <csparams-reqid>`, :ref:`type <csparams-type>`,
  :ref:`handle <csparams-handle>`, :ref:`authinfo <csparams-authinfo>`

Email type: ``expiration_notify``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the domain owner in response to the domain expiration
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`
* additional parameter concerning ENUM domains:
  :ref:`valdate <csparams-valdate>`

Email type: ``expiration_dns_owner``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the domain owner in response to the exclusion of the domain from zone
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`
* additional parameter concerning ENUM domains:
  :ref:`valdate <csparams-valdate>`

Email type: ``expiration_register_owner``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the domain owner in response to the upcoming domain cancellation
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`
* additional parameter concerning ENUM domains:
  :ref:`valdate <csparams-valdate>`

Email type: ``expiration_dns_tech``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the technical contacts of the nsset whose domain was just excluded
  from zone
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`
* additional parameter concerning ENUM domains:
  :ref:`valdate <csparams-valdate>`

Email type: ``expiration_register_tech``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the technical contacts of the nsset whose domain was just cancelled
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`
* additional parameter concerning ENUM domains:
  :ref:`valdate <csparams-valdate>`

Email type: ``expiration_validation_before``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the owner of an ENUM domain in response to the upcoming expiry
  of domain's validation
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`valdate <csparams-valdate>`

Email type: ``expiration_validation``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent to the owner of the ENUM domain in response to the expiry
  of domain's validation
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`checkdate <csparams-checkdate>`,
  :ref:`domain <csparams-domain>`,
  :ref:`owner <csparams-owner>`,
  :ref:`nsset <csparams-nsset>`,
  :ref:`exdate <csparams-exdate>`,
  :ref:`dnsdate <csparams-dnsdate>`,
  :ref:`exregdate <csparams-exregdate>`,
  :ref:`statechangedate <csparams-statechangedate>`,
  :ref:`registrar <csparams-registrar>`,
  :ref:`valdate <csparams-valdate>`

Email type: ``notification_create``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent when a new object (domain, contact, nsset, keyset) is created,
  to the email contact of the created object
* common passed parameters:  :ref:`defaults.* <csparams-defaults>`,
  :ref:`ticket <csparams-ticket>`, :ref:`registrar <csparams-registrar>`,
  :ref:`handle <csparams-handle>`, :ref:`type <csparams-type>`

* additional parameters concerning new objects:
   * ``fresh.object.authinfo`` – transfer password

* additional parameters concerning a new **contact**:
   * ``fresh.contact.name`` – name of contact person
   * ``fresh.contact.org`` – organization name
   * ``fresh.contact.address.permanent`` – permanent personal address / organization
     headquarters address
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
  (nsset, domain, keyset).

Email type: ``notification_update``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent after an object (domain, contact, nsset, keyset)
  is updated, to the email contact of the updated object
* common passed parameters:  :ref:`defaults.* <csparams-defaults>`,
  :ref:`ticket <csparams-ticket>`, :ref:`registrar <csparams-registrar>`,
  :ref:`handle <csparams-handle>`, :ref:`type <csparams-type>`

* additional parameters concerning changes in an object:

   * ``changes`` – general indication of changes: ``0`` – there are **no**
     changes, ``1`` – there are some changes
   * Whether a change has occured or not, is indicated for each attribute
     of an object and parameters containing both the old and the new
     value of the attribute are passed in the following manner:

      * ``changes.*.attribute`` indicates a change in an attribute
        – if the attribute has changed, it contains the value "``1``";
        otherwise the parameter is not passed,
      * ``changes.*.attribute.old`` contains the value of the attribute
        before the change (passed only if the attribute has changed),
      * ``changes.*.attribute.new`` contains the value of the attribute
        after the change (passed only if the attribute has changed).

   * ``changes.object.authinfo`` – indicates that the object's transfer
     password has changed,
   * Indication of changes of other attributes is specific for each object type
     as follows.

* additional parameters concerning changes in a **contact**:
   * ``changes.contact.name`` – contact name has changed
   * ``changes.contact.org`` – organization name has changed
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
   * ``changes.contact.telephone`` – phone number has changed
   * ``changes.contact.fax`` – fax number has changed
   * ``changes.contact.email`` – email address has changed
   * ``changes.contact.notify_email`` – notification email address has changed
   * ``changes.contact.ident_type`` – type of personal identification has
     changed
   * ``changes.contact.ident`` – personal identifier has changed
   * ``changes.contact.vat`` – VAT-payer registration number (DIČ) has changed
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
* additional parameters concerning changes in a **nsset**:
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
* additional parameters concerning changes in a **domain**:
   * ``changes.domain.registrant`` – domain owner has changed
   * ``changes.domain.nsset`` – nsset assignment has changed
   * ``changes.domain.keyset`` – keyset assignment has changed
   * ``changes.domain.admin_c`` – list of administrative contacts has changed
   * ``changes.domain.val_ex_date`` :sup:`ENUM` – date of validation expiry
     has changed
   * ``changes.domain.publish`` :sup:`ENUM` – publication in telephone
     directory has changed
* additional parameters concerning changes in a **keyset**:
   * ``changes.keyset.tech_c`` – list of technical contacts has changed
   * ``changes.keyset.dnskey`` – list of DNS keys has changed


Email type: ``notification_transfer``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent after an object (domain, contact, nsset, keyset) is transferred
  to a new registrar, to the email contact of the transferred object
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`ticket <csparams-ticket>`, :ref:`registrar <csparams-registrar>`,
  :ref:`handle <csparams-handle>`, :ref:`type <csparams-type>`

Email type: ``notification_renew``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent after a domain is renewed, to its owner's email
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`ticket <csparams-ticket>`, :ref:`registrar <csparams-registrar>`,
  :ref:`handle <csparams-handle>`, :ref:`type <csparams-type>`

Email type: ``notification_unused``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent after an unused object (contact, keyset, nsset) is removed
  from the database, to the email contact of the removed object
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`ticket <csparams-ticket>`, :ref:`registrar <csparams-registrar>`,
  :ref:`handle <csparams-handle>`, :ref:`type <csparams-type>`

Email type: ``notification_delete``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* sent after an object (domain, contact, nsset, keyset) is deleted,
  to the email contact of the deleted object
* passed parameters: :ref:`defaults.* <csparams-defaults>`,
  :ref:`ticket <csparams-ticket>`, :ref:`registrar <csparams-registrar>`,
  :ref:`handle <csparams-handle>`, :ref:`type <csparams-type>`


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

* ``defaults.company`` – name of the company operating the Registry
* ``defaults.street`` – street in the headquarters address of the company
  operating the Registry
* ``defaults.postalcode`` – postal code in the headquarters address of the
  company operating the Registry
* ``defaults.city`` – city in the headquarters address of the company operating
  the Registry
* ``defaults.tel`` – phone contact of the company operating the Registry
* ``defaults.fax`` – fax contact of the company operating the Registry
* ``defaults.emailsupport`` – email contact of the technical support
* ``defaults.authinfopage`` – URL of the site from which the end users can
  request the transfer password (authinfo)
* ``defaults.whoispage`` – URL of the site from which the public can search
  in the Registry
* ``defaults.company_cs`` – Czech variant of the name of the company
  operating the Registry
* ``defaults.company_en`` – English variant of the name of the company
  operating the Registry

Common parameters
~~~~~~~~~~~~~~~~~

   .. _csparams-authinfo:

   ``authinfo``
      transfer password

   .. _csparams-checkdate:

   ``checkdate``
      the date when the object-state check was performed and this email created
      (according to the server's local time, date format: YYYY-MM-DD)

   .. _csparams-dnsdate:

   ``dnsdate``
      date from which the domain will not be included in the zone anymore

   .. _csparams-domain:

   ``domain``
      handle of the domain in question

   .. _csparams-exdate:

   ``exdate``
      date of domain expiration (till when the registration has been prepaid)

   .. _csparams-exregdate:

   ``exregdate``
      date from which the domain can be registered by another subject
      (domain is unguarded)

   .. _csparams-handle:

   ``handle``
      string object identifier

   .. _csparams-owner:

   ``owner``
      identifier of the owner of the domain in question (contact handle)

   .. _csparams-nsset:

   ``nsset``
      identifier of the name server set assigned to the domain in question
      (nsset handle)

   .. _csparams-registrar:

   ``registrar``
      name and website of the current sponsoring registrar
      (in case of transfer, the new sponsoring registrar)

   .. _csparams-reqdate:

   ``reqdate``
      the date when the request was placed (date format dd.mm.YYYY)

   .. _csparams-reqid:

   ``reqid``
      the identification number of the request by which it can be traced
      in the Registry

   .. _csparams-statechangedate:

   ``statechangedate``
      date when the respective object state was set

   .. _csparams-ticket:

   ``ticket``
      email identifier

   .. _csparams-type:

   ``type``
      object type by number: ``1`` – contact, ``2`` – nsset, ``3`` – domain, ``4`` – keyset

   .. _csparams-valdate:

   ``valdate``
      date till when the ENUM domain has been validated
