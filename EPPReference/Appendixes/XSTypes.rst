


XMLSchema-defined data types
============================

Simple data types defined in the XML Schema :doc:`namespace
</EPPReference/SchemasNamespaces/index>`.

.. glossary::
   :sorted:

   xs:string
      a generic non-restricted character string

      https://www.w3.org/TR/xmlschema11-2/#string

   xs:normalizedString
      a :term:`xs:string` which does not contain carriage return, line feed
      nor tab characters

      https://www.w3.org/TR/xmlschema11-2/#normalizedString

   xs:token
      a :term:`xs:normalizedString` which has no leading nor trailing spaces
      and no internal sequence of 2 or more spaces

      https://www.w3.org/TR/xmlschema11-2/#token

   xs:boolean
      ``True``/``False`` or ``1``/``0``

      https://www.w3.org/TR/xmlschema11-2/#boolean

   xs:language
      a :term:`xs:token` matching the ``[a-zA-Z]{1,8}(-[a-zA-Z0-9]{1,8})*``
      pattern

      https://www.w3.org/TR/xmlschema11-2/#language

   xs:anyURI
      an Internationalized Resource Identifier reference (IRI)

      https://www.w3.org/TR/xmlschema11-2/#anyURI

   xs:dateTime
      a date and time

      https://www.w3.org/TR/xmlschema11-2/#dateTime

   xs:date
      a date

      https://www.w3.org/TR/xmlschema11-2/#date

   xs:decimal
      a real number represented by decimal numerals (low precision)

      https://www.w3.org/TR/xmlschema11-2/#decimal

   xs:unsignedLong
      a potentially big non-negative integer

      https://www.w3.org/TR/xmlschema11-2/#unsignedLong

   xs:unsignedShort
      an average non-negative integer

      https://www.w3.org/TR/xmlschema11-2/#unsignedShort

   xs:unsignedByte
      a small non-negative integer (up to 255 incl.)

      https://www.w3.org/TR/xmlschema11-2/#unsignedByte

   xs:base64Binary
      binary data represented in Base64 encoding, see :rfc:`4648#section-4`

      https://www.w3.org/TR/xmlschema11-2/#base64Binary
