
.. _error-reasons:

Error reasons
=============

If a :ref:`response <struct-response>` was returned with an error result code,
the response may also contain a reason that explains further why the error occurred.

The reason is provided in the language of :doc:`the session
</EPPReference/CommandStructure/Login>`.

Possible reasons of errors are:

.. in older versions including FRED 2.29:

#. bad format of contact handle
#. bad format of nsset handle
#. bad format of fqdn domain
#. Domain name not applicable.
#. invalid format
#. already registered.
#. within protection period.
#. Invalid IP address.
#. Invalid nameserver hostname.
#. Duplicate nameserver address.
#. Glue IP address not allowed here.
#. At least two nameservers required.
#. invalid date of period
#. period exceedes maximal allowed validity time.
#. period is not aligned with allowed step.
#. Unknown country code
#. Unknown message ID
#. Validation expiration date can not be used here.
#. Validation expiration date does not match registry data.
#. Validation expiration date is required.
#. Can not remove nameserver.
#. Can not add nameserver
#. Can not remove technical contact
#. Technical contact is already assigned to this object.
#. Technical contact does not exist
#. Administrative contact is already assigned to this object.
#. Administrative contact does not exist
#. nsset handle does not exist.
#. contact handle of registrant does not exist.
#. Nameserver is already set to this nsset.
#. Nameserver is not set to this nsset.
#. Expiration date does not match registry data.
#. Attribute op in element transfer is missing
#. Attribute type in element ident is missing
#. Attribute msgID in element poll is missing
#. Registration is prohibited
#. Schemas validity error:
#. Duplicity contact
#. Bad format of keyset handle
#. Keyset handle does not exist
#. DSRecord does not exists
#. Can not remove DSRecord
#. Duplicity DSRecord
#. DSRecord already exists for this keyset
#. DSRecord is not set for this keyset
#. Field \`\`digest type'' must be 1 (SHA-1)
#. Digest must be 40 characters long
#. Object does not belong to the registrar
#. Too many technical administrators contacts.
#. Too many DS records
#. Too many DNSKEY records
#. Too many nameservers in this nsset
#. No DNSKey record
#. Field \`\`flags'' must be 0, 256 or 257
#. Field \`\`protocol'' must be 3
#. Unsupported value of field "alg", see http://www.iana.org/assignments/dns-sec-alg-numbers
#. Field \`\`key'' has invalid length
#. Field \`\`key'' contains invalid character
#. DNSKey already exists for this keyset
#. DNSKey does not exist for this keyset
#. Duplicity DNSKey
#. Keyset must have DNSKey or DSRecord
#. Duplicated nameserver hostname
#. Administrative contact not assigned to this object
#. Temporary contacts are obsolete

.. from version FRED 2.32:

   #. An invalid format of the contact handle
   #. An invalid format of the nsset handle
   #. An invalid format of the domain name
   #. The domain name not applicable
   #. An invalid format
   #. Registered already
   #. Within the protection period
   #. An invalid IP address
   #. An invalid nameserver hostname
   #. A duplicate nameserver address
   #. Glue IP address not applicable
   #. The validity period exceeds the allowed maximum
   #. The validity period is not an integer multiple of the allowed step
   #. An unknown country code
   #. An unknown message ID
   #. A validation expiration date not applicable
   #. The validation expiration date is not valid
   #. The technical contact cannot be removed
   #. The technical contact is assigned to the object already
   #. The technical contact does not exist
   #. The administrative contact is assigned to the object already
   #. The administrative contact does not exist
   #. The nsset does not exist
   #. The registrant contact does not exist
   #. The nameserver is included in the nsset already
   #. The nameserver is not included in the nsset
   #. The domain expiration date does not match recorded data
   #. The "transfer" element is missing an "op" attribute
   #. The "ident" element is missing a "type" attribute
   #. The "poll" element is missing an "msgID" attribute
   #. Registration is prohibited
   #. XML validation error:
   #. A duplicate contact
   #. An invalid format of the keyset handle
   #. The keyset does not exist
   #. Unauthorized access to the object
   #. Too many administrative contacts
   #. Too many DS records
   #. Too many DNSKEY records
   #. No DNSKEY record
   #. The "flags" field must be 0, 256 or 257
   #. The "protocol" field must be 3
   #. An unsupported value of the "alg" field, see IANA DNS Security Algorithm Numbers
   #. The "key" field has an invalid length
   #. The "key" field contains an invalid character
   #. The DNSKEY exists for the keyset already
   #. The DNSKEY does not exist for the keyset
   #. A duplicate DNSKEY
   #. The keyset must have a DNSKEY record or a DS record
   #. A duplicate nameserver hostname
   #. The administrative contact is not assigned to the object
   #. Temporary contacts are discontinued
   #. The validity period is shorter than the allowed minimum
