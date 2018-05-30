


Rules for setting automatic flags
=================================

This section describes the formal rules for automatic flag setting.

Legend:

* ``<name>`` the parameter which is queried from the ``enum_parameters`` table with the ``name`` key
* ``[...]`` unit of measure for the preceding parameter
* ``current_date`` the current date (calculated from the timestamp within the time zone of the database server)
* ``current_timestamp`` the current date and time (within the time zone of the database server)
* ``current_timestamp at time zone <...>`` conversion of the current date and time into the time zone specified within ``<...>``

.. _rules-regex:

Domain registration expiration rules
------------------------------------

Legend:

* ``regexdate`` the date when a domain expires (``domain.exdate``)

.. code-block:: none
   :caption: expirationWarning

   regexdate + <expiration_notify_period> [days] <= current_date
      && !serverRenewProhibited


.. code-block:: none
   :caption: expired

   regexdate <= current_date
      && !serverRenewProhibited


.. code-block:: none
   :caption: unguarded

   regexdate + <expiration_dns_protection_period> [days] + <regular_day_outzone_procedure_period> [hours]
      <= current_timestamp at time zone <regular_day_procedure_zone>
      && !serverRenewProhibited


.. code-block:: none
   :caption: nssetMissing

   nsset is not assigned


.. code-block:: none
   :caption: outzone

   nssetMissing
      || serverOutzoneManual
      || !serverInzoneManual && (unguarded || notValidated)


.. code-block:: none
   :caption: outzoneUnguardedWarning

   regexdate + <outzone_unguarded_email_warning_period> [days]
      <= current_timestamp at time zone <regular_day_procedure_zone>
      && !serverRenewProhibited
      && !serverInzoneManual


.. code-block:: none
   :caption: outzoneUnguarded

   unguarded && !serverInzoneManual


.. code-block:: none
   :caption: deleteWarning

   regexdate + <expiration_letter_warning_period> <= current_date
       && !serverRenewProhibited


.. code-block:: none
   :caption: deleteCandidate

   regexdate + <expiration_registration_protection_period> [days] + <regular_day_procedure_period> [hours]
      <= current_timestamp at time zone <regular_day_procedure_zone>
      && !serverRenewProhibited
      && !serverDeletePohibited

.. _rules-valex:

ENUM domain validation rules
----------------------------

Legend:

* ``valexdate`` the date till which an ENUM domain is validated (``enumval.exdate``)

.. code-block:: none
   :caption: validationWarning1

   valexdate + <validation_notify1_period> [days] <= current_date


.. code-block:: none
   :caption: validationWarning2

   valexdate + <validation_notify2_period> [days] <= current_date


.. code-block:: none
   :caption: notValidated

   valexdate + <regular_day_outzone_procedure_period> [hours]
      <= current_timestamp at time zone <regular_day_procedure_zone>

.. _rules-obsol:

Non-domain obsoletion rules
---------------------------

Legend:

* ``last_linked_timestamp`` the timestamp when this was linked to another object the last time
* ``update`` the date of the last update
* ``crdate`` the date of creation

.. code-block:: none
   :caption: deleteCandidate

   max(last_linked_timestamp, update, crdate)
      + <object_registration_protection_period> [months]
      + <regular_day_procedure_period> [hours]
      <= current_timestamp at time zone <regular_day_procedure_zone>
      && !serverDeleteProhibited
      && !linked
