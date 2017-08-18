


FRED-defined data types
=======================

Used simple data types defined in the FRED namespaces.

.. glossary::
   :sorted:

   fredcom:authInfoType
      a :term:`xs:normalizedString` of the length between 0 and 300 characters

   fredcom:objIDType
      a :term:`xs:token` of the length between 1 and 63 characters

   fredcom:objIDCreateType
      a :term:`xs:token` of the length between 1 and 30 characters
      matching the ``[a-zA-Z0-9](-?[a-zA-Z0-9])*`` pattern

   fredcom:objIDChgType
      a :term:`xs:token` of the length between 0 and 63 characters

   fredcom:msgType
      an unbounded :term:`xs:normalizedString`

   fred:amountType
      a :term:`xs:decimal` of the maximum length of 10 digits
      of which at most 2 digits are the fraction

   domain:pLimitType
      an :term:`xs:unsignedShort` ranging from 1 to 99 (inclusive)

   domain:trIDStringType
      a :term:`xs:token` of the length between 3 and 64 characters

   contact:identValueT
      a :term:`xs:token` of the maximum length of 32 characters

   contact:vatT
      a :term:`xs:token` of the maximum length of 20 characters

   contact:emailType
      a single email address (a :term:`xs:token`
      matching the ``[^@]{1,64}@[^@]+`` pattern
      and having the maximum length of 320 characters)

   contact:emailCommaListType
      a comma-separated list of email addresses (a :term:`xs:token`
      matching the ``[^@, ]{1,64}@[^@, ]+(,[^@, ]{1,64}@[^@, ]+)*`` pattern
      and having the maximum length of 320 characters)

   contact:emailUpdCommaListType
      a comma-separated list of email addresses, empty string allowed
      (a :term:`xs:token`
      matching the ``([^@, ]{1,64}@[^@, ]+(,[^@, ]{1,64}@[^@, ]+)*)?`` pattern
      and having the length between 0 and 320 characters)

   contact:e164StringType
      a phone number in the international format without spaces
      and the national prefix separated from the rest with a period
      (a :term:`xs:token` matching the ``(\+[0-9]{1,3}\.[0-9]{1,14})?`` pattern
      and having the maximum length of 17 characters)

   contact:postalLineType
      a :term:`xs:normalizedString` of the length between 1 and 255 characters

   contact:optPostalLineType
      a :term:`xs:normalizedString` of the length between 0 and 255 characters

   contact:pcType
      a :term:`xs:token` of the maximum length of 16 characters

   contact:ccType
      a :term:`xs:token` of the length of 2 characters

   nsset:addrStringType
      a :term:`xs:token` of the length between 3 and 45 characters

   nsset:reportlevelType
      an :term:`xs:unsignedByte` ranging from 0 to 10 (inclusive)

   nsset:trIDStringType
      a :term:`xs:token` of the length between 3 and 64 characters

   keyset:keyT
      a :term:`xs:base64Binary` string, non-empty
