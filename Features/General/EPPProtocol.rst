


EPP protocol
------------

The registrars communicate with the Registry using the EPP protocol
(:rfc:`5730`)
with extensions for individual objects.
The extensions are slightly modified versions of the standard specifications
for domains (:rfc:`5731`) and contacts (:rfc:`5733`).

The FRED contains unique extensions for nssets and keysets.

Beside the standard commands, there are further auxiliary
functions, such as information about credit or bulk list operations.

EPP communication is secured by the standard login-and-password authentication
together with the verification of a client SSL certificate.

To ease EPP communication, the FRED distribution contains
a `Python <http://www.python.org/>`_ client library
and a command-line client application.
