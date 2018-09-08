:orphan:

Considerations for upgrade to FRED 2.38
=======================================

.. rubric:: Registry operator (Daphne users)

Saved search filters in Daphne will be removed with the database upgrade.
You will have to re-create them and save them again.

.. rubric:: Registrars

Registrars will have to upgrade the CLI EPP client.


Payments processing
-------------------

.. rubric:: Registry operator

If you have been using FRED's payments processing as it is, you should know
that Daphne doesn't provide pairing of payments anymore. This function was moved
to Django PAIN.

If you have been using the part of billing in FRED, which is performed
by transproc calls of fred-admin and WebAdmin (payment processing & pairing),
you should consider installing two new components: ``django-pain``
and ``fred-pain``, upgrading ``transproc`` and using ``django-pain`` web admin.

Also, you need to migrate payments to PAIN database:

* :file:`upgrades/2.34.0-2.35.0-01.sql` -- add ``UUID`` column to ``bank_payment`` table
  (among other upgrades)
* :file:`upgrades/2.34.0-2.35.0-02-superuser-dump-table.sql`
   - exports bank accounts to CSV
   - exports payments to JSON -- fix escaping in the output file with the command::

      sed -e "s/\\\\/\\/g" /var/lib/postgresql/payments-export-for-pain.json > /var/lib/postgresql/payments-export-for-pain-fixed.json

* copy the fixed JSON to the PAIN node
* run PAIN migration script, such as::

   PYTHONPATH=$PYTHONPATH:/etc/ferda
   DJANGO_SETTINGS_MODULE=pain_cfg.settings
   migrate_payments_from_FRED.py < payments-export-for-pain-fixed.json

  - migration is logged with the standard PAIN log
  - migration script can be run repeatedly, previously imported payments are skipped

* :file:`upgrades/2.34.0-2.35.0-03-drop-table.sql` -- drop payments tables from FRED.

Disclosure configuration
---------------------------

.. rubric:: Registry operator

:doc:`Disclosure policy of the EPP server </EPPReference/PoliciesRules>` is
:ref:`configurable <config-contact-disclosure>` at last!

You should add new configuration values in your ``fred-rifd`` (back end)
and ``mod-eppd`` (front end) configuration files after the upgrade.
At least the ``contact_data_filter`` and default disclosure flags for attributes
absent in the schemas should be configured, otherwise contact creation and
update will fail.

.. rubric:: The public

Remember that the disclosure preferences affect, which contact information
can be seen in **WHOIS** and **RDAP**.
