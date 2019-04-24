
Customizing PDF templates
-------------------------

The Portable Document Format (PDF) is used for many documents exported
by the system such as letters (expiration warning), invoices
or the portion of public requests delivered by post.

These documents are rendered with the :program:`fred-doc2pdf` script from RML
(`Report Markup Language <http://www.reportlab.com/software/rml-reference/>`_),
which is an XML-based intermediary format for PDF rendering.

Intermediary RML files are constructed from dynamic XML data (generated from
the database) and *static strings* stored in XML files in the same folder
as templates. Standard XSLT templates and an XSLT processor are employed
to construct these intermediary files.

The templates (.xsl) can be found in the directory
:file:`@PREFIX@/share/fred-doc2pdf/templates/`.

The *static strings* (.xml) are available in Czech and English localizations and
the localization is selected in each template with the ``lang`` parameter.

The easiest way to customize PDFs is to **adapt the headers and footers**
to match your corporate identity (logo and graphic design). The default design
(used in CZ.NIC) is in the ``cznic_design.xsl`` template, which is imported
by all other templates.
