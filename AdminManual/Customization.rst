
.. _FRED-Admin-Custom:

Customization
=========================

.. only:: mode_structure

   .. struct-start

   **Sources:** WEB/Docs + IVIEW + translate :ref:`??? <src>`
   | **AoW:** done & unplanned

   **Chapter outline:**

   * email template (parameters)
   * default header/footer
   * letter template (parameters)
      * expiration letters

   .. struct-end

.. NOTE adapt database values (like template translation) in db init script

The customization of the FRED mainly concerns the generated announcements,
notifications and exported PDFs.

.. contents:: Chapter TOC
   :local:

Email templates
---------------
Email templates are located in the database tables :file:`mail_type`
(email subject) and :file:`mail_templates` (email body).

We recommend to replace the Czech variant of texts with the variant in your
language and keep the English variant for common understanding.

Texts are processed with the `ClearSilver <http://www.clearsilver.net/>`_
tool which takes a template and passed parameters and creates the resulting
email text.

There is a set of parameters which are passed to all emails (*defaults.\**)
but the passing of other parameters depends on the type of email.
For a detailed reference of the passed parameters according to email type see
:ref:`FRED-Admin-App-CSParams`.

.. NOTE
   Header - table: mail_header_defaults ?
   Footer - table: mail_footer ?
   (cs) defaults.* - table:mail_defaults

PDF templates
----------------

The Portable Document Format (PDF) is used for many documents exported
by the system such as letters (expiration warning), invoices
or the portion of public requests delivered by post.

These documents are rendered by the :program:`fred-doc2pdf` script from RML
(`Report Markup Language <http://www.reportlab.com/software/rml-reference/>`_)
which is an XML-based intermediary format for PDF rendering.

Intermediary RML files are constructed from dynamic XML data (generated from
the database) and static strings stored in XML files in the same folder
as templates. Standard XSLT templates and an XSLT processor are employed
to construct these intermediary files.

The templates (.xsl) can be found in the directory
:file:`@PREFIX@/share/fred-doc2pdf/templates/`.

The static strings (.xml) are available in Czech and English localizations and
the localization is selected in each template with the ``lang`` parameter.

.. todo:: What must be done for a new localization?
   static strings + modify templates?

The easiest way to customize PDFs is to **adapt the headers and footers**
to match your corporate identity (logo and graphic design). The default design
(used in CZ.NIC) is in the ``cznic_design.xsl`` template which is imported
into the other templates.
