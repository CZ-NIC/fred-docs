
.. _FRED-Admin-RegInit:

Registry initialization
==================================

.. only:: mode_structure

   .. struct-start

   **Sources:** NOTES :ref:`??? <src>` 
   | **AoW:** (1 day) for CR + *1 day*

   **Chapter outline:**

   * Setting up a zone
   * Setting up Registrars
   * Setting up the invoicing subsystem
     (price list, invoice numbering, VAT tax, credit)

   .. struct-end

   -----

This chapter will help you initialize the Registry, i.e. introduce the crucial data that must be present in the system prior to registrations or
any work with registrable objects.

It is assumed that you have already installed the FRED's database schema
and that the database is blank (you have not input any data yet).

To initialize the Registry, you need to perform these tasks:

* prepare a zone:

   * create a zone,
   * assign name servers to the zone,

* prepare registrars:

   * add registrar(s),
   * set authentication data for registrar(s),
   * grant registrars access to the zone(s),

* prepare the accounting subsystem:

   * create a price list for operations,
   * define the parameters for invoice numbering,
   * set the VAT tax and coefficient,
   * assign credit to registrars.

* set some parameters.

..  Important:: Perform the tasks in the same order as presented!

For most tasks, the :program:`fred-admin` command-line utility is used.
The commands of this utility have both mandatory and optional parameters.
The mandatory parameters are marked with an asterisk (*) and
default values are stated for the optional parameters.
If you omit an optional parameter, the default value is assigned.

.. Note:: The presented listings of parameters are only illustrative
   and often incomplete. To see all available commands and parameters,
   refer to ``fred-admin --help``.

.. contents:: Chapter TOC
   :local:

.. _FRED-Admin-reginit-zone:

Preparing a zone
----------------

Preparing a zone is the most crucial task. The information you enter
about a zone, will appear in the header of a generated zone file.
When you create a zone, you enter the fields of the SOA record,
and in the next step, you add the zone name servers.
An example of the resulting zone file header is given
:ref:`below <FRED-Admin-reginit-zone-example>`.

.. _FRED-Admin-reginit-zone-add:

Creating a zone
^^^^^^^^^^^^^^^
.. code:: bash

   $ fred-admin --zone_add \
      --zone_fqdn=cz \
      --ex_period_min=12 \
      --ex_period_max=120 \
      --ttl=18000 \
      --hostmaster=hostmaster@nic.cz \
      --refresh=900 \
      --update_retr=300 \
      --expiry=604800 \
      --minimum=900 \
      --ns_fqdn=a.ns.nic.cz

This command creates a new zone in the Registry.
It does not have to be only a TLD zone of course, you might provide access
for example to **go.to**, **com.tw** or ENUM zones (like **0.2.4.e164.arpa**).

.. Important:: Consider thoroughly which parameters you set,
   there is no command for editing zones.

* ``--zone_fqdn`` (*) – FQDN of the zone to be added
  – it also serves as a key in subsequent commands
* ``--ex_period_min``, ``--ex_period_max`` – minimum and maximum number
  of months for which a domain in the zone can be registered

  .. Note:: The ``ex_period_min`` number is also used as a unit
     for registration periods which are then defined as multiples
     of this number, i.e. with ``--ex_period_min=12`` domains can be
     registered (and renewed) for whole years, not e.g. year and half.

  Defaults:

  - ``--ex_period_min=12`` [months]
  - ``--ex_period_max=120`` [months]

* ``--ttl``, ``--hostmaster``, ``--refresh``, ``--update_retr``, ``--expiry``,
  ``--minimum``, ``--ns_fqdn`` – zone's SOA fields

  Defaults:

  - ``--ttl=18000`` [s]
  - ``--hostmaster=hostmaster@localhost``
  - ``--refresh=900`` [s]
  - ``--update_retr=300`` [s]
  - ``--expiry=604800`` [s]
  - ``--minimum=900``
  - ``--ns_fqdn=localhost``

.. NOTE Vychozi hodnoty by mely byt v referencni prirucce a zde jen odkaz.

.. _FRED-Admin-reginit-zone-ns:

Adding zone name servers
^^^^^^^^^^^^^^^^^^^^^^^^
.. code:: bash

   $ fred-admin --zone_ns_add --zone_fqdn=cz --ns_fqdn=a.ns.nic.cz
   $ fred-admin --zone_ns_add --zone_fqdn=cz --ns_fqdn=b.ns.nic.cz --addr=1.2.3.4
   $ fred-admin --zone_ns_add --zone_fqdn=cz --ns_fqdn=c.ns.nic.cz --addr=5.6.7.8,9.0.1.2

This command assigns a name server to a zone.

* ``--zone_fqdn`` (*) – the zone a name server is added to
* ``--ns_fqdn`` (*) – name server's FQDN – fully qualified domain name
* ``--addr`` – name server's IP address (glue) – it is required when the name server's FQDN is from the same zone to which it is added; you can list several IP addresses separated by a comma

.. Note:: The name servers are not tested, only saved to the database.

.. _FRED-Admin-reginit-zone-example:

Zone file example
^^^^^^^^^^^^^^^^^
The data given in the examples above result in the following zone file header:

.. code:: bash

   $TTL 18000 ;default TTL for all records in zone
   cz.             IN      SOA     a.ns.nic.cz.    hostmaster.nic.cz. (1445442458 900 300 604800 900)
                   IN      NS      a.ns.nic.cz.
                   IN      NS      b.ns.nic.cz.
                   IN      NS      c.ns.nic.cz.
   b.ns.nic.cz.    IN      A       1.2.3.4
   c.ns.nic.cz.    IN      A       5.6.7.8
   c.ns.nic.cz.    IN      A       9.0.1.2
   ;
   ;--- domain records ---
   ;



.. _FRED-Admin-reginit-reg:

Preparing registrars
--------------------

.. only:: mode_structure

   .. todo:: Explain system/common reg. in Features, then rewrite

There are two types of registrars:

* a **common registrar** is an organization which provides domain
  administration to end-users and pays for access to the Registry, and
* the **system registrar** which is used by the Registry to manage
  domains manually and to perform automated administration procedures.

Both types of registrars are prepared in the same way:

* create a registrar,
* assign them authentication data,
* permit them to operate in a zone (or zones).

.. Important:: For the system to work properly, exactly one system registrar
   must be present.

.. Tip::

   .. only:: mode_structure

      .. todo:: rewrite

   If you want to work only with the EPP communication, the system
   registrar will do. However, if it is the billing and invoicing subsystem
   you want to work with, we recommend adding a (testing) common registrar, too.

Creating a registrar
^^^^^^^^^^^^^^^^^^^^
.. code:: bash

   # adding a common registrar:
   $ fred-admin --registrar_add \
      --handle=REG-FRED_A --reg_name="Testing registrar A" \
      --organization="Company l.t.d." --country=CZ

   # adding a system registrar:
   $ fred-admin --registrar_add \
      --handle=REG-SYS --reg_name="System registrar" \
      --country=CZ --system

This command creates a new registrar with some data.

* ``--handle`` (*) – handle of the registrar to be added
* ``--reg_name`` – registrar's name – you may set it the same as ``--organization``
* ``--organization`` – registrar's organization or company
* ``--country`` (*) – registrar's country by 2-letter country code (table enum_country)
* ``--no_vat`` – flag this registrar as NOT a :term:`VAT`-payer
* ``--system`` – designates this registrar to be the "system registrar"
* many other parameters are available, see the program help.

.. Note:: Registrar information can be edited later via the WebAdmin.

Setting authentication data
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Authentication data allows registrars to connect to the Registry securely.

.. code:: bash

   $ fred-admin --registrar_acl_add \
      --handle=REG-FRED_A \
      --certificate="39:D1:0C:CA:05:3A:CC:C0:0B:EC:6F:3F:81:0D:C7:9E" \
      --password=passwd

This command assigns the given access control data to a registrar.

* ``--handle`` (*) – registrar's handle
* ``--password`` (*) – registrar's password – both the password and
  certificate are needed to access the Registry
* ``--certificate`` (*) – fingerprint of the registrar's certificate

  It can be created from an existing certificate with the following command::

     $ openssl x509 -noout -fingerprint -md5 -in /path/to/cert.pem | cut -d= -f2

.. Note:: For testing purposes, you can use the test certificate that comes
   with the :file:`fred-mod-eppd` package and was installed
   in :file:`{$PREFIX}/share/fred-mod-eppd/ssl/`.

   .. Tip:: If that is the case, you can copy & paste the fingerprint
      from this example.

.. NOTE On production, registrars are asked to supply their own certificate
   which is usually signed by a qualified certification authority.
   (In CZ there are 3 official qualif. CAs. Consult your local authorities
   to enquire about applicable legislation.)
   Another approach is to create your own certification authority
   and prepare certificates for your registrars yourself,
   see `Registrar certification`_


Granting access to a zone
^^^^^^^^^^^^^^^^^^^^^^^^^
.. code:: bash

   $ fred-admin --registrar_add_zone \
      --zone_fqdn=cz --handle=REG-FRED_A \
      --from_date="2007-01-01"

This command grants a registrar permissions to manage objects in a specified zone.

* ``--handle`` (*) – registrar's handle
* ``--zone_fqdn`` (*) – name of a zone the registrar gains access to
* ``--from_date`` – date since when is the access allowed – default: today


Preparing the accounting subsystem
----------------------------------

The accounting subsystem allows you to set prices for operations,
charge Registrars for these operations, keep track of their credit
and create bills (invoices) for them.

All these functions are built-in and on by default.

You can **turn charging off**: find the ``[rifd]`` section in the server
configuration and set ``epp_operations_charging = false``. Then you don't
need to do anything else from this section and you can skip the rest of it.

Otherwise you need to prepare the subsystem for use by doing these tasks:

* create a price list for operations,
* define initial numbers for invoice numbering,
* set a custom VAT tax rate,
* assign initial credit to common registrars.


Creating price list
^^^^^^^^^^^^^^^^^^^
A price list is created by listing prices for operations individually.
The price lists are defined for each zone separately.

.. _list-charge-ops:

Chargeable operations include:

.. https://admin.nic.cz/wiki/developers/fred/accounting#%C3%9A%C4%8Dtovan%C3%A9polo%C5%BEky

* ``CreateDomain`` – domain registration (one-time payment when a new domain
  is introduced to the Registry, corresponding EPP command: create_domain),
  pricing period: one-time
* ``RenewDomain`` – domain renewal (renewal per unit, corresponding
  EPP commands: create_domain, renew_domain), pricing period:
  per unit (:ref:`ex_period_min <FRED-Admin-reginit-zone-add>`)

.. QUESTION RenewDomain - per unit nebo natvrdo per year?

* ``GeneralEppOperation`` – operation over request-usage limit (charged only
  after all uncharged requests were exhausted), pricing period: per operation

..
   * [Future?] ``Fine`` – minimum advancement for operations in a zone, pricing period: per year
   * [Future?] ``Fee`` – fee for the access to a zone, pricing period: per year


.. code:: bash

   $ fred-admin --price_add --operation='CreateDomain' --zone_fqdn=cz \
      --valid_from='2014-12-31 23:00:00' \
      --operation_price 0 --period 1

   $ fred-admin --price_add --operation='RenewDomain' --zone_fqdn=cz \
      --valid_from='2014-12-31 23:00:00' --valid_to='2015-01-31 22:59:59' \
      --operation_price 155 --period 1

   $ fred-admin --price_add --operation='RenewDomain' \
      --valid_from='2015-01-31 23:00:00' --zone_fqdn=cz \
      --operation_price 140 --period 1

   $ fred-admin --price_add --operation='RenewDomain' --zone_fqdn=cz \
      --valid_from='2015-09-01 19:15:56.159594' --valid_to='2015-12-31 23:00:00' \
      --operation_price 190 --period 1

   $ fred-admin --price_add --operation='GeneralEppOperation' \
      --valid_from='2015-05-31 22:00:00' --zone_fqdn=cz \
      --operation_price 0.10 --period 1 --enable_postpaid_operation

This command adds a price of an operation in a zone valid in a given time span.
The amount is currency-independent, decimals are allowed.
If you don't want to charge for an operation, just set the price to zero.

* ``--valid_from``, ``--valid_to`` – range of UTC datetimes when the pricing
  scheme will be used, e.g. '2006-09-09 19:15:56', valid_from < valid_to
* ``--operation_price`` (*) – amount, e.g. 140.00
* ``--period`` – pricing period/quantity (default = 1)
* ``--zone_fqdn`` (*) – zone FQDN
* ``--operation`` (*) – charged operation
* ``--enable_postpaid_operation`` – operation charge doesn't require prepaid
  credit (allows negative credit)

.. Note:: The first domain renewal is made upon domain creation, therefore
   a registration of a new domain is in fact billed as 2 operations:
   ``CreateDomain + RenewDomain`` whereas the renewal of an existing domain
   is billed only as one operation ``RenewDomain``.


Invoice numbering
^^^^^^^^^^^^^^^^^
To allow the invoices to be numbered automatically, *initial numbers* must
be defined for each invoice type, zone and year. An initial number is
then incremented on invoice creation and the updated value is kept
in the database for future reference.

You have two ways of defining initial invoice numbers:

* you can set invoice prefixes and let the system create the initial numbers
  following the fixed pattern **PPYY00001**:

   * **PP** – 2-digit invoice number prefix
   * **YY** – 2 last digits of a year
   * **00001** – the 5-digit order number

   .. Tip:: This way is recommended if you have many zones to administer.

* you can set custom initial numbers manually.


Creating default initial numbers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code:: bash

   $ fred-admin --add_invoice_number_prefix \
      --prefix=24 --zone_fqdn=cz --invoice_type_name=advance
   $ fred-admin --add_invoice_number_prefix \
      --prefix=23 --zone_fqdn=cz --invoice_type_name=account

.. only:: mode_structure

   .. todo:: Explain invoice types in Features, then rewrite

This command adds a number prefix for invoices of a given type in a zone.

* ``--prefix`` – the prefix value for the given combination of a zone and
  invoice type
* ``--zone_fqdn`` – the zone FQDN for which the prefix is designated
* ``--invoice_type_name`` – the invoice type by name:

   * ``account`` – billing (balance between the deposit and the total
     for provided services), usually monthly (?)

   .. vyúčtování

   * ``advance`` – depositing credit, when a payment was received (?)

   .. zálohová faktura

.. code:: bash

   $ fred-admin --create_invoice_prefixes --for_current_year

This command creates initial invoice numbers for all available combinations
for the current year. If the ``--for_current_year`` argument is omitted,
initial numbers are created for the next year.

Defining custom initial numbers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. only:: mode_structure

   .. todo:: QUESTION Is okay or deprecated?

.. code:: bash

   $ fred-admin --invoice_add_prefix --zone_fqdn=cz --type 0 --year 2017 --prefix 401700001

This command adds a custom initial number (prefix) for the given combination
of a year, zone and invoice type (0 – advance, 1 – account).


Value-added tax
^^^^^^^^^^^^^^^
To add your own VAT tax rate, you must know three things:

* the rate percentage,
* the rate coefficient and
* when the validity of the previous rate ends.

The percentage (PERC) is usually given by the law, e.g. 21 %. So is the period
of validity. The coefficient (COEF) is the officially correct way
(in the Czech Republic) to figure out the tax basis and therefore it is used
in calculations. You can calculate the coefficient with the following formula:
``PERC / (PERC + 100) = COEF`` and the result is then rounded to four decimal
places, e.g. for 21 % VAT: 21 / (21 + 100) = 0.1736.

Since there is no command to change the VAT rate, you must run an SQL script
directly:

.. code:: bash

   $ psql -U fred
   fred=> begin;
   update price_vat set valid_to = '2014-12-31 23:00:00' where valid_to is null;
   insert into price_vat (koef,vat) values (0.1736,21) ;
   commit ;

This SQL script will:

* end the validity of the last rate to the specified date time in UTC,
* add the new coefficient and the new percentage.


Assigning credit to a registrar
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code:: bash

   $ fred-admin --invoice_credit \
      --zone_id=1 --registrar_id=1 --price=15000

This command adds some credit to a registrar in a zone and creates an advance
invoice in the system. If the registrar is a VAT-payer, then an appropriate
amount is subtracted automatically.

* ``--zone_id`` – zone id,
* ``--registrar_id`` – registrar id,
* ``--price`` – the credit to add,
* ``--taxdate`` – tax date, default is today, for arg format
  see ``fred-admin --help_dates``

.. Tip:: To find an *id* of a zone or a registrar, you must run an SQL query
   against the database, for example:

   .. code:: bash

       $ psql -U fred -c "SELECT id FROM registrar where handle = 'REG-FRED_A';"

   This command will find a registrar by its handle and return its identifier.

   .. code:: bash

       $ psql -U fred -c "SELECT id FROM zone where fqdn = 'cz';"

   This command will find a zone by its FQDN and return its identifier.


Setting parameters in the database
----------------------------------
..  enum_parameters.regular_day_procedure_zone

There is a table of customizable parameters in the main database.
The most of them can be used with the default values, however the following
parameter **must** be adapted to your environment:

* the appropriate time zone for automated administration
  – **regular_day_procedure_zone**::

   $ fred-admin --enum_parameter_change \
      --parameter_name=regular_day_procedure_zone \
      --parameter_value=TZNAME

  where TZNAME is the standardized name of your time zone which can be found
  in the Postgres table ``pg_timezone_names`` (the *name* column) or
  `in this list <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones>`_
  (the *TZ* column), for example ``Europe/Prague`` (this is the default value).

.. only:: mode_structure

   .. todo:: You can customize also other parameters from this table,
      see :ref:`blablabla <todo-link>` (the reference).
