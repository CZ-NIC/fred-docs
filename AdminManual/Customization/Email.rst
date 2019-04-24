
Customizing email templates
---------------------------

Email templates are used to generate automatic Registry email communication,
such as notifications and warnings.

**The templates can me modified through SQL queries.** Emails are decomposed
into several database tables as follows.

.. Important:: **If you customize database tables, remember to examine changes
   in the database component before upgrading the FRED!**

   Sometimes we need to edit the templates for ourselves and these changes are
   added to a database upgrade script, which would overwrite your settings.
   Therefore you should either **backup** your current database tables to recover
   your settings after the upgrade, **or adapt** the upgrade script directly,
   so that you don't lose your settings.

.. contents:: Chapter TOC
   :local:
   :backlinks: none



.. _custom-email-registry:

Registry contact information (defaults)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Table: ``mail_template_default``

This table contains Registry contact information (called ``defaults``)
grouped in the JSON form.

``defaults.*`` are a data subset that is passed to all email templates.

The parameters are described :ref:`in the parameter reference <csparams-defaults>`.

.. code-block:: json
   :caption: Example: Registry information JSON

   {
      "defaults.company": "CZ.NIC, z. s. p. o.",
      "defaults.company_cs": "CZ.NIC, správce domény CZ",
      "defaults.company_en": "CZ.NIC, the CZ domain registry",
      "defaults.emailsupport": "podpora@nic.cz",
      "defaults.tel": "+420 222 745 111",
      "defaults.street": "Milešovská 1136/5",
      "defaults.city": "Praha 3",
      "defaults.postalcode": "130 00",
      "defaults.whoispage": "https://www.nic.cz/whois",
      "defaults.authinfopage": "http://www.nic.cz/whois/publicrequest/",
      "defaults.registrarlistpage": "https://www.nic.cz/whois/registrars"
   }

You may have several defaults and associate each with an email template
by referencing it in the ``mail_template.mail_template_default_id`` attribute.



.. _custom-email-types:

Email types
^^^^^^^^^^^

Table: ``mail_type``

This table maps an email type ``name``, which is referred to in the
:ref:`FRED-Admin-App-CSParams`, to an ``id`` referenced by the ``mail_template``
table.

Each email type serves a specific purpose that is built in into the overall
functionality of the Registry. For this reason, there is no easy way of adding
custom email types at the moment, although you may easily customize the existing
types.

It is also possible to disable sending of some email types,
see :doc:`/AdminManual/Customization/Notifications`.

Email types are briefly described in the :doc:`/AdminManual/Appendixes/EmailParameters`.



.. _custom-email-compose:

Email composition
^^^^^^^^^^^^^^^^^^

An email message is composed of:

* header fields,
* a subject,
* a body,
* a footer at the end of the body,
* vCard attachment.

.. _custom-email-compose-head:

Email headers
~~~~~~~~~~~~~

Table: ``mail_header_default``

This table allows you to preset email header fields, namely:

* ``h_from`` -- sender address, ``From`` header, e.g. ``support@registry.com``
  or ``"Registry Support" <support@registry.com>``,
* ``h_replyto`` -- address that should be used to reply, ``Reply-To`` header,
* ``h_errorsto`` -- address(es) for additional notification of delivery errors,
  ``Errors-To`` header,
* ``h_organization`` -- sender organization, ``Organization`` header,
* ``h_contentencoding`` -- content encoding for the ``Content-Type`` header,
  e.g. ``charset=UTF-8``,
* ``h_messageidserver`` -- hostname that will be used to generate the
  ``Message-ID`` header, e.g. ``registry.com``, which will result in Message IDs
  like ``<39370682.1555751410@registry.com>``.

You may have several sets of headers. To associate one with an email template,
reference it in the ``mail_template.mail_header_default_id`` attribute.

.. rubric:: Message-ID generation

A complete Message-ID is composed in the following manner::

   <mail_archive.id>.<int(epoch_time)>@<mail_header_default.h_messageidserver>

.. _custom-email-compose-foot:

Email footers
~~~~~~~~~~~~~

Table: ``mail_template_footer``

This table allows you to preset email footers.

An email footer is a component of email content that is added right after the body,
typically used to include uniformly-formatted :ref:`Registry contact information
<custom-email-registry>`. For example:

.. code-block:: none
   :caption: Email footer example

   --
   <?cs var:defaults.company ?>
   <?cs var:defaults.street ?>
   <?cs var:defaults.postalcode ?> <?cs var:defaults.city ?>
   ---------------------------------
   phone: <?cs var:defaults.tel ?>
   email: <?cs var:defaults.emailsupport ?>
   ---------------------------------

You may have several footers. To associate one with an email template,
reference it in the ``mail_template.mail_template_footer_id`` attribute.

.. _custom-email-compose-vcard:

Email vCards
~~~~~~~~~~~~~

Table: ``mail_vcard``

This table contains a unique Registry vCard that is inserted by Mailer to all emails
as an attachment.

You may redefine it by updating the row. VCard version is not restricted by the FRED,
it is up to you to decide which to use, just consider compatibility with email clients.

.. code-block:: none
   :caption: vCard example

   BEGIN:VCARD
   VERSION:2.1
   N:podpora CZ.NIC, z. s. p. o.
   FN:podpora CZ.NIC, z. s. p. o.
   ORG:CZ.NIC, z. s. p. o.
   TITLE:zákaznická podpora
   TEL;WORK;VOICE:+420 222 745 111
   ADR;WORK:;;Milešovská 1136/5;Praha 3;;130 00;Česká republika
   URL;WORK:http://www.nic.cz
   EMAIL;PREF;INTERNET:podpora@nic.cz
   REV:20161108T120000Z
   END:VCARD



.. _custom-email-compose-body:

Email template bodies
~~~~~~~~~~~~~~~~~~~~~

Table: ``mail_template``

This table contains the core of the email templates, and it has the following attributes:

* ``mail_type_id`` -- reference to a mail type ``id`` from ``mail_type``,
* ``version`` -- version number of the template (see below),
* ``subject`` -- a short description of message content for the ``Subject`` header,
* ``body_template`` -- the main part of a template, see :ref:`custom-email-templating`,
* ``body_template_content_type`` -- content subtype of the message (only ``plain`` is tested),
* ``mail_template_footer_id`` -- reference to a footer ``id`` from ``mail_template_footer``,
* ``mail_template_default_id`` -- reference to a defaults ``id`` from ``mail_template_default``,
* ``mail_header_default_id`` -- reference to a headers ``id`` from ``mail_header_default``,
* ``created_at`` -- template creation timestamp.

.. rubric:: Subject

We use the convention ``Local-language subject text / English subject text``.
Feel free to adapt the local-language text. If you decide to change the optical
separator (``/``), you should use it consistently across the email types.

.. rubric:: Content type

The general content type of an email body is always ``text``.
The ``body_template_content_type`` attribute is a subtype, usually ``plain``,
therefore the full content type results in ``text/plain``. Other text subtypes
are theoretically possible (such as html, css, xml, csv), although only ``plain``
has been tested!

.. rubric:: Versioning

- The last version is used in generation of new emails.
- Older versions are kept to regenerate archived messages for viewing
  in the WebAdmin.
- When you're changing any attribute of a mail template, **insert a new row**
  with the change and with the version number incremented by 1.

.. Tip:: To write upgrades, you may use our database functions
   ``get_current_mail_template_version(mail_type_id)``
   and/or ``get_next_mail_template_version(mail_type_id)``.

.. _custom-email-templating:

Body templating
^^^^^^^^^^^^^^^

In the email body template, we use the convention: local-language (Czech) text
first, English text second,
and the language variants are optically separated with a couple of newlines.

.. Note:: We recommend to replace the Czech variant of texts with the variant
   in your local language and keep the English variant for common understanding.

Email bodies are processed with the `ClearSilver <http://www.clearsilver.net/>`_
template system, which takes a template in plain text and passes it
a data set to create a resulting email.
Each email template is passed a different data set, which depends on the email type.
Data (parameters) are passed to a template in a hierarchical form.
To traverse the hierarchy, a dot convention is used.

ClearSilver lets you do some basic templating:

* Output the value of a variable:

  .. code-block:: xml
     :caption: ClearSilver example: Variable

     Handle: <?cs var:handle ?>

* Control the flow:

  .. code-block:: xml
     :caption: ClearSilver example: Conditional expression

     <?cs if:ident_type != "" ?>
      <?cs
      if:ident_type == "OP"?>Personal ID: <?cs
      elif:ident_type == "PASS"?>Passport number: <?cs
      elif:ident_type == "BIRTHDAY"?>Date of birth: <?cs
      /if ?> <?cs var:ident_value ?>
     <?cs /if ?>

* Iterate over a list:

  .. code-block:: xml
     :caption: ClearSilver example: List iteration

     <?cs each:item = administrators ?>Administrative contact: <?cs var:item ?>
     <?cs /each ?>

* And more.

See `templates in ClearSilver <http://www.clearsilver.net/docs/man_templates.hdf>`_
for complete syntax reference.

For a detailed reference of the passed parameters according to the email type see
:doc:`/AdminManual/Appendixes/EmailParameters`.


..
   Email archiving
   ^^^^^^^^^^^^^^^^

   Table: ``mail_archive``
