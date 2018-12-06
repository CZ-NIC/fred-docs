


Contacts
========

Contacts are a type of :term:`registrable object`\ s which represents a natural
or legal person in the Registry.

The FRED understands a contact without a value in the *organization* attribute
as a natural person for the purpose of disclosure.

See also :doc:`attributes of contacts (EPP Reference) </EPPReference/ManagedObjects/Contacts>`
for a description of contact details.

.. _contact-roles:

Roles of linked contacts
------------------------

Contacts can have the following roles depending on the type of the registrable
object to which they are linked:

* the domain holder,
* an administrative contact of a domain,
* a technical contact of an nsset or a keyset.

The *domain holder* may request any modification of their domain, including the change
of the domain holder.
An *administrative contact* may request any modification of the domain except the
change of the domain holder. See also :doc:`attributes of domains (EPP Reference)
</EPPReference/ManagedObjects/Domains>`.

A *technical contact* may request any modification of the linked nsset or keyset.
See also :doc:`attributes of nssets (EPP Reference) </EPPReference/ManagedObjects/Nssets>`
or :doc:`attributes of keysets (EPP Reference) </EPPReference/ManagedObjects/Keysets>`.

A single contact can appear in several roles.

.. _contact-reminder:

Annual reminder
---------------

Contacts themselves are responsible for completeness, accuracy and recency
of their contact details.

To keep contact information updated, contacts should be called on by email once a year
to check their details and correct them if there was a change.

This can be set as a :ref:`periodic task <cronjob-contact-reminder>` in the FRED.

.. _contact-disclosure:

Disclosure of information
-------------------------

The Registry defines policies for disclosure of contact information in the
public interface (whois services):

* the general approach ("Registry shows information" vs. "Registry hides information"),
* disclosure of which attributes registrars will be allowed to manipulate
  (signal the contact's preference opposite to the general approach), and
* default disclosure settings if no preference is requested
  (show or hide per attribute).

All of this can be :ref:`configured <config-contact-disclosure>`.

.. :term:`CZ-specific` Disclosure settings of some attributes may be conditional.
