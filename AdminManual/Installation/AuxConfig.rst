
.. _set-pg:

Setting timezone in PostgreSQL
------------------------------

The FRED assumes database connections using UTC timezone, so configure
PostgreSQL to handle connections using this timezone.

Open :file:`/etc/postgresql/9.1/main/postgresql.conf` with a text editor
and change the **timezone** parameter to ``UTC``, or use a script like this::

   sudo sed -i~ -e "s/^#\?\s*timezone\s*=.*/timezone = 'UTC'/" \
      /etc/postgresql/9.1/main/postgresql.conf

Then restart PostgreSQL::

   sudo service postgresql restart
