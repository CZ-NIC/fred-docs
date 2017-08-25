


Technical checks
================

The system allows to check the technical state of name servers and report
the results to the administrators of the name servers or registrars.

A technical check consists of one or more tests with graded severity of failure.
Only if a test of higher severity passed, then a test of lower severity is performed.
The severity of a test is described by a number on the scale from 0 to 10;
the lower the number, the higher the severity of a test.

Each nsset may contain information about the severity that should be tested (the *report level*)
but this can be overridden when a check is being requested via the EPP interface. If neither provides
this information, the default level is tested (FRED's default: 3).
Currently, there are no level-0 tests and the highest level in use is 6.

.. Note:: The tests are only informative,
   they do not affect the inclusion/exclusion of a domain in/from the zone.

.. NOTE test `glue_ok` is not described in the Rules

Specific tests and their dependencies are described in the `Technical communication rules
<https://www.nic.cz/files/nic/doc/Communication_rules_20111001.pdf>`_ (PDF).
