:orphan:

Considerations for upgrade to FRED 2.39
=======================================

.. rubric:: Registry operator

Due to the new attribute ``UUID``, the database needs extensions
from the package ``postgresql-contrib-9.6``:

- install the package with extensions
- create extensions with `2.35.1-2.36.0-01-create-extension-superuser.sql
  <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.35.1-2.36.0-01-create-extension-superuser.sql>`_
- run Python script `2.35.1-2.36.0-02-uuid.py
  <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.35.1-2.36.0-02-uuid.py>`_
- run it again to add integrity constraints
- trigram indexes with `2.35.1-2.36.0-03-trigram-indexes.sql
  <https://github.com/CZ-NIC/fred-db/blob/master/upgrades/2.35.1-2.36.0-03-trigram-indexes.sql>`_
