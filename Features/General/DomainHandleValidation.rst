


Domain name & handle format validation
-----------------------------------------

The FRED implements several standard rules for domain name format validation:

* forbid consecutive hyphens,
* forbid empty domain name,
* enforce :rfc:`1035` preferred syntax,
* enforce single digit labels (for ENUM domains),
* forbid IDN punycode encoding.

The rules can be :ref:`configured per zone <config-dn>`.

If the Registry operator requires additional restrictions, they can be implemented
by providing forbidden keywords or patterns in the domain blacklist.
The :ref:`restrictions can be configured <config-restrict-dn>` for any period
of time given by a starting and ending date of validity.

The Registry operator can also :ref:`configure the format of handles
<config-handles>` of contacts, nssets and keysets, and they can do it for each
object type separately.
