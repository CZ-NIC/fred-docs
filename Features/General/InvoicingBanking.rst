


Invoicing and banking
---------------------

The FRED implements the prepaid-invoicing model. 

Bank accounts are queried for incoming payments using out-of-the-box scripts
and these payments are matched to Registrars using pairing symbols. 
If a payment matches, an advance invoice is issued and credit is extended
to the matching Registrar by a corresponding amount. 
The credit is then decreased upon each domain registration or renewal.
The price of registration and renewal is configurable per zone.

At some point in time, it's possible to create an accounting invoice
for a particular Registrar containing a list of all its registrations
and renewals and the total amount of money subtracted from the credit. 

.. Warning::

   Work with the accounting subsystem might be a little tricky
   because it is tightly tied to the context of the financial and commercial
   laws of the Czech Republic (esp. the :term:`VAT` handling and invoice 
   essentials).
   Therefore it may not be fully (or at all) suitable for your environment.

.. todo:: negative credit
