
.. index::
   pair: renew; domain


Renew domain
============

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

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.

.. rubric:: Example

.. code-block:: xml

   <epp/>
