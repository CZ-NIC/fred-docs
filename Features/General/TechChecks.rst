


Technical checks
----------------

There are several technical checks that are performed on registered
name servers to diagnose potential domain delegation problems.
Those checks are completely informational and they do not block
the registration process.

Technical checks are invoked regularly in a configurable interval and
their results are sent using email to contacts associated with name servers.

They can also be invoked on demand by a Registrar using the EPP interface.
In this case, results are sent back to the Registrar via the EPP poll mechanism.

The checks include existence and reachability of name servers, 
presence of delegated domains on name servers or the authoritative
flag of DNS answers for such domains. 
