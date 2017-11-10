


Automatic keyset management
---------------------------

In order to simplify introduction and rotation of DNSSEC keys, the FRED implements
two standards devised for key management automation: :rfc:`7344` and :rfc:`8078`.
By polling domains' name servers for CDNSKEY records, the Registry can easily
link DNSSEC-enabled domains into the global chain of trust and respond to key updates flexibly.
This method does not require registrars to be involved in any way
because the publishing of the CDNSKEY records relies on DNS operators.

:doc:`More on the concept of automatic keyset management. </Features/Concepts/AKM>`
