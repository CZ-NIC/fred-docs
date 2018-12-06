


Billing
=======

Billing in the FRED is targeted at **registrars**, who are charged for various operations,
such as registrations, renewals, or the annual fee. The FRED supports both *prepaid*
and *postpaid* model, which can be configured *per operation*.

A virtual account is managed for each registrar, which holds just the amount
of **credit** without a specific currency. Incoming payments increase the credit
on this account and charging for operations decreases it. The current state
of credit is available over EPP. An account is kept for each zone separately.

.. rubric:: Payment model

If a charged operation has the **prepaid model** associated with it, it **fails**
when there is not enough credit (EPP response code: :code:`2104 Billing failure`).
Therefore registrars must pay in advance to use these operations.

If a charged operation has the **postpaid model** associated with it, it **succeeds**
even when there is not enough credit.
Therefore registrars do not have to pay in advance.
This situation can create debt and it is up to the Registry to force registrars
to pay it off.

Each operation can have a different model. Generally, setting the model means
to (dis)allow negative credit.

.. contents:: Chapter TOC
   :local:
   :backlinks: none

Scanning bank transactions
--------------------------

The idea is to run periodical scans for payments on bank accounts of the Registry operator.

The FRED contains :term:`CZ-specific` scripts (connectors) to process transcripts
of transactions collected from several banks that operate in the Czech Republic.
(To study the scripts may help you in writing your custom connectors.)

Each bank has a B2B interface or API, but the individual banks use various channels
(HTTP, IMAP) and various formats (CSV, XML). Therefore there is a specialized script
for each bank, which transforms the payments into a common format
and loads it into the FRED database.

A registrar can be identified in each payment with a payment symbol, which
is given to them by the Registry operator, and which the registrar must enter
with the bank transaction. If the symbol in a transaction matches a registrar,
the payment is associated with this registrar. Unmatched transactions may be
:ref:`associated manually <daphne-task-assign-payment>` in the web administration (Daphne).

.. versionchanged:: 2.38
   Bank transactions are collected, parsed and associated with registrars externally,
   and imported to FRED via a new Accounting interface for further processing.
   See also :doc:`PAIN`.

Processing payments
-------------------

Once the payment is associated, the money can be processed further.
If the registrar has debt, the money is used to cover the debt. The remaining amount,
or all of it if there was no debt, is accepted as an **advance payment**.

For an advance payment, an invoice is issued to the registrar. (This is based
on a legal requirement in CZ. It may not be necessary in another environment,
but it is hard-coded.)

Then the :term:`VAT` is subtracted from the amount.

.. Note:: VAT percentage can be :ref:`configured <reginit-vat>`.

.. Note:: VAT subtraction applies to registrars who are marked as VAT-payers.
   The FRED marks registrars as VAT-payers by default.
   They can be unmarked (designated as not VAT-payers) individually:

   * either with the ``--no_vat`` argument when :ref:`adding a new registrar
     <reginit-newreg>` with :program:`fred-admin`, or
   * by unchecking the ``DPH`` checkbox in :ref:`registrar details
     <daphne-task-registrar-edit>` in :program:`Daphne`.

.. Tip:: To disable the VAT completely:

   * set all registrars as not VAT-payers, or
   * configure VAT percentage to 0 %.

After that, the (VAT-reduced) amount is added to credit.

.. Tip:: Credit can be added for the registrar even without having to scan
   for bank transactions. Just use the CLI tool :program:`fred-admin`
   to :ref:`assign credit to a registrar <reginit-credit>`.

Charging by a price list
------------------------

The FRED has a configurable **price list** for operations that require charging:

* establishment of a new domain record (:code:`CreateDomain`) via EPP,
* prolongation of an existing domain record (:code:`RenewDomain`) via EPP,
* EPP requests over a limit (:code:`GeneralEppOperation`).

This can be configured through the CLI tool :program:`fred-admin`,
see :ref:`reginit-price-list`. Prices are set for each zone separately.
A price can be valid for a limited time (validity period).

.. rubric:: Charging for specific EPP requests

Registrars are charged when EPP commands are carried out, for EPP commands:

* :code:`renew_domain` – charged for one operation: prolongation only, and
* :code:`create_domain` – charged for 2 operations: establishment and immediate prolongation.

Establishment is charged one time, whereas prolongation is multiplied
by the length of the registration period. For example: If prices are
*CreateDomain for USD 4* and *RenewDomain for USD 6*,
then creating a new domain registration for 2 years costs ``4 + (2 * 6) = USD 16``,
and renewing an existing domain for 3 years costs ``3 * 6 = USD 18``.

The amount is subtracted from credit.
In the prepaid model, if there is not enough credit, the command fails.

.. rubric:: Charging for all EPP requests over a limit :sup:`OPTIONAL`

Each registrar has an individual monthly limit of free EPP transactions based
on the number of registered domains. (There is a minimum for beginner registrars.)
At the end of a month, we count transactions and charge for the difference over
the limit [#reqcount]_. The amount is subtracted from credit. If there is not enough credit,
we still charge in negative credit.

Tasks: Call :code:`fred-admin --charge_request_fee` before monthly billing
:code:`fred-admin --invoice_billing ...`.

.. [#reqcount] Transactions (except poll req/ack) are counted for all object types
   and for all zones together, but they are billed with the zone configured in the table
   ``request_fee_parameter.zone_id`` by the price that is configured for this zone
   and this operation in the price list.

.. rubric:: Other charges

Other charges can be implemented only as custom SQL scripts, but it is risky!

For example, the Czech Registry charges additionally:

* *an annual fee for zone access* (:code:`Fee`):

  Once a year, we inform registrars to increase credit, first, and then we subtract
  the annual fee (USD 3,000) from the credit. If there is not enough credit, we still
  charge in negative credit.

* *a fine for too few registrations* (:code:`Fine`):

  Each registrar must register for at least USD 7,000 per year (new domains or renewals).
  At the end of a year, we count the current state and if there is a difference,
  we charge for the difference under the minimum. This is not subtracted from
  credit, but it is covered by the next payment.

Both these charges, however, are made manually with ad-hoc scripts,
which are not released with the FRED.

Invoicing
---------

There are 2 types of invoices stored in the FRED database: advance (for advance payments)
and account (monthly bills).
Invoices are automatically numbered, but initial numbers (per year and invoice type)
must be configured before invoices can be generated, see :ref:`reginit-invoice-numbering`.

Invoices are delivered to registrars' email in both XML and PDF formats. The XML format is
FRED's format for invoices and it can be transformed with XSLT for import
into accounting software. The PDF format is generated with a templating system.

Customization options
---------------------------

* Configure prepaid/postpaid model per operation
* Configure price list and VAT
* Write custom connectors for bank systems or add credit manually
* Invoices can be ignored or :ref:`PDF templates must be adapted <custom-pdf>`
* Write XSL transformations to upload invoices to accounting software
