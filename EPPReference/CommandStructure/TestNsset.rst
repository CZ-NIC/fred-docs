
.. index:: keyword

Test nsset
===========

Command for requesting technical checks (tests) over nssets.

The check is not performed immediately but it is scheduled for execution.
After the tests have finished, results are provided to the client
in the :ref:`poll messages <struct-poll-test>`.

Command element structure
-------------------------

.. rubric:: Example

.. code-block:: xml

   <epp/>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > cmd

Response element structure
--------------------------

.. rubric:: Example

.. code-block:: xml

   <epp/>
