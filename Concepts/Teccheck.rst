


Technical checks
================

The system allows to check the technical state of name servers and report
results to administrators of the name servers or registrars.

Technical checks are performed periodically and/or on demand from registrars.

A technical check consists of one or more individual tests with graded
severity which are applied to a name server within a name-server set
in a certain order. Some tests focus on the basic functionality of a name server
and others on greater details which, if not satisfied, do not actually
jeopardise domain delegation.

.. Note:: The tests are only informative,
   they do not affect inclusion/exclusion of a domain in/from a zone.

Each test has a unique name that describes the name-server property
to be tested. Test severity indicates the significance of failure of a given
test. Severity is represented by an integer number on the scale from 0 to 10.
The lower the number, the higher the severity of a test.

Only if a test of higher severity passed, then a test of lower severity is
performed.

The test result is one of the following:

- Test passed
- Test failed
- Unknown result

The *unknown result* represents a situation in which the test ended
in an unexpected error or unexpected circumstance that prevented achievement
of a passed/failed result.

Each nsset may contain information about the *severity level* that should be
tested for it (the ``report level`` attribute) but this can be overridden
when a check is being requested by a registrar via the EPP interface.
If neither provides this information, the default level is tested
(FRED's default: 3, configurable).
Currently, there are no level-0 tests and the highest level in use is 6.

.. list-table:: Individual tests
   :header-rows: 1
   :widths: 15, 7, 18, 60

   * - Test name
     - Severity
     - Depends on
     - Description
   * - Glue_OK
     - 1
     -
     - Tests whether there is a glue record when required for a given DNS server and domains.
   * - Existence
     - 1
     - Glue_OK
     - Tests whether the DNS server is running.
   * - Presence
     - 2
     - Glue_OK, Existence
     - Tests the presence of the record of the domain on the DNS server.
   * - Authoritative
     - 3
     - Glue_OK, Existence, Presence
     - Tests whether the DNS server's response to a particular domain is authoritative.
   * - NotRecursive
     - 4
     - Glue_OK, Existence
     - Tests whether the DNS server is recursive based on what the DNS server says about itself.
   * - NotRecursive4all
     - 4
     - Glue_OK, Existence
     - Tests whether the DNS server is recursive based on a practical test.
   * - Autonomous
     - 5
     - Glue_OK, Existence
     - At least two of the DNS servers must be in different autonomous systems.
   * - Heterogeneous
     - 6
     - Glue_OK, Existence
     - At least two DNS servers with different software.

If a check is requested by a registrar via EPP, the results are delivered
to the registrar in a :ref:`EPP poll message <epp-poll-type-techcheck>`.

If a periodic check fails, technical contacts of an nsset are :ref:`notified by
email <email-type-techcheck>` which informs also about the cause of the failure.


.. todo:: TecCheck execution - Algorithm description ?
   :class: todo-backlog
