:orphan:

Considerations for upgrade to FRED 2.39
=======================================

.. rubric:: Registry operator

Due to UUID (for Ferda) Database needs extensions from package ``postgresql-contrib-9.6``

- install package
- create extensions https://gitlab.office.nic.cz/fred/db/blob/master/upgrades/2.35.1-2.36.0-01-create-extension-superuser.sql
- run python script https://gitlab.office.nic.cz/fred/db/blob/master/upgrades/2.35.1-2.36.0-02-uuid.py
- run it again to add integrity constraints
- ... https://trac.nic.cz/ticket/24362

.. rubric:: Registrars

...

.. rubric:: The public

...
