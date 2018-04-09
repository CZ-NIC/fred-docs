


Technical checks
----------------

Technical checks are informative tests performed on registered
name servers to diagnose potential domain delegation problems.

The technical checks are invoked regularly in a configurable interval and
their results are sent using email to contacts associated with name servers.

They can also be invoked on demand by a registrar using the EPP interface.
In this case, results are sent back to the registrar via the EPP poll mechanism.

The tests include existence and reachability of name servers,
presence of delegated domains on name servers or the authoritative
flag of DNS answers for such domains.

:doc:`More on the concept of technical checks. </Concepts/Teccheck>`
