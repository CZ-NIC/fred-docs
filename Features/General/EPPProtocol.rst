


EPP protocol
------------

The Registrars communicate with the Registry using the EPP protocol 
(`RFC 5730 <https://tools.ietf.org/html/rfc5730>`_) 
with extensions for individual objects. 
The extensions are slightly modified versions of the standard specifications 
for domains (`RFC 5731 <https://tools.ietf.org/html/rfc5731>`_) 
and contacts (`RFC 5733 <https://tools.ietf.org/html/rfc5733>`_). 

The FRED contains unique extensions for the NSSets and KeySets. 

EPP communication is secured by the standard login-and-password authentication
together with the verification of a client SSL certificate. 

To ease EPP communication, the FRED distribution contains 
a `Python <http://www.python.org/>`_ client library
and a command-line client application.
