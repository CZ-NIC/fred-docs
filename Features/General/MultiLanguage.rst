


Multi-language support & IDN
----------------------------

The FRED is UTF8-aware within all its subsystems.
Supported languages are very easily extensible by means of a standard process
of language-catalogues manipulation.

Internationalized Domain Names (IDN) are supported in the system core
as a configuration option that can be turned on, so that domains in UTF-8
can be registered and displayed, however there are limitations:

* there is no way of restricting the character set,
* there are no bindings of IDN and non-IDN domains.
