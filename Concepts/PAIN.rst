The Future of Payments & Invoices
=================================

We are aware that the :doc:`original billing subsystem <Billing>` in FRED
may not be suitable for use in other countries as it is.
Therefore we have decided to detach this subsystem from FRED and leave
billing to other tools as much as possible.

This detachment will be done in several phases and the *phase 1* is
part of FRED 2.38 (see below).

.. rubric:: The target state

The intention is to remove payments (bank transactions) collection, parsing,
registrar association, :term:`VAT` calculations and invoicing from FRED.

Payments will be processed by an external tool which will interface
with both FRED and an accounting system that should handle invoices, VAT
and currencies properly.

FRED will only keep the currency-neutral credit account for each registrar
and provide an interface for increasing and decreasing credit amount.

It will be up to the Registry operator which accounting system
they choose and how they interconnect it with FRED.

.. rubric:: The state of affairs in version 2.38

Scanning for payments, parsing and association with registrars is done
in an external tool that calls FRED's Accounting interface (IDL)
to import payment data for further processing: to handle credit and generate invoices,
because they remain in FRED for now. FRED handles credit internally,
there is no interface yet.

The external tool we use in the Czech Registry is :program:`Django PAIN`,
which we started to develop for our own accounting purposes. This tool
is released to the public along with FRED, but it is :term:`CZ-specific`
and is intended only as an example implementation for inspiration or customization.
When we reach the target state, we will provide some customization instructions.

See also :doc:`/ReleaseNotes/Upgrade-2-38`.
