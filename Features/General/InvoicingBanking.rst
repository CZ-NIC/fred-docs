


Invoicing and banking :sup:`CZ-specific`
------------------------------------------

The FRED implements both the prepaid-invoicing and postpaid-invoicing model
which can be selected for each billed operation.

Payments collected by an external system can be paired with FRED using the
Accounting interface. When a payment is paired, an advance invoice is issued
and credit is extended to the matching registrar by a corresponding amount.
The credit is then decreased upon each domain registration or renewal.
The price of registration and renewal is configurable per zone.

At some point in time, it's possible to create an accounting invoice
for a particular registrar containing a list of all its registrations
and renewals and the total amount of money subtracted from the credit.

.. Note::

   Work with the billing subsystem may be tricky
   because it is tightly tied to the context of the financial and commercial
   laws of the Czech Republic (esp. the :term:`VAT` handling and invoice
   essentials).

   Therefore it may not be fully (or at all) suitable for your environment.

More about :doc:`billing in FRED </Concepts/Billing>`.

There is also a new concept of billing being developed, see :doc:`/Concepts/PAIN`.
