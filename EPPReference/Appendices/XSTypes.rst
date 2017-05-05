


XMLSchema-defined data types
============================

Used simple data types defined in the XML Schema namespace.

.. glossary::
   :sorted:

   xs:string
      a character string
      https://www.w3.org/TR/xmlschema11-2/#string

   xs:normalizedString
      a :term:`xs:string` which does not contain carriage return, line feed
      nor tab characters
      https://www.w3.org/TR/xmlschema11-2/#normalizedString

   xs:token
      a :term:`xs:normalizedString` which...
      https://www.w3.org/TR/xmlschema11-2/#token

   xs:boolean
      ``True``/``False`` or ``1``/``0`` https://www.w3.org/TR/xmlschema11-2/#boolean

   xs:language
      a :term:`xs:token` matching the ``[a-zA-Z]{1,8}(-[a-zA-Z0-9]{1,8})*``
      pattern
      https://www.w3.org/TR/xmlschema11-2/#language

   xs:anyURI
      an Internationalized Resource Identifier Reference (IRI)
      https://www.w3.org/TR/xmlschema11-2/#anyURI

   xs:dateTime
      https://www.w3.org/TR/xmlschema11-2/#dateTime
