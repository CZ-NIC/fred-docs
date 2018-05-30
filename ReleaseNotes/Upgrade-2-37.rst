:orphan:


Considerations for upgrade to FRED 2.37
=======================================

.. rubric:: Registry operator

:doc:`Policies of the EPP server </EPPReference/PoliciesRules>` are hard-coded
in this version. If the new policies do not suit your needs, wait for a future
version that will make these policies configurable.

Because we needed to hide most of personal information in the production database
that used to be shown, we created a utility that can reset disclosure preferences
in existing contacts.
We have used the utility ``fred-disclose-flags-update`` to reset disclose flags
according to these rules (ignoring former preferences):

* Hide all attributes except *name*, *organization*, and *address*.
* If a contact (of a natural person) is verified, hide *address*, too.

Note that these rules also apply when new contacts are created and when they
become verified, and that these rules are part of the hard-coded policies.

Whether you will reset the disclose flags of existing contacts or not, and how,
is up to you, as it is not necessary.

.. rubric:: Registrars

If you decide to upgrade, your registrars will need to check that their
**custom EPP client** programs are able to work with ``flag="1"`` when:

* interpreting disclosure preference described in responses to ``contact:info``,
* requesting disclosure preference with ``contact:create`` and ``contact:update``,

and adapt them, eventually.

If they use **fred-client**, they just need to upgrade to the version 2.10,
which can deal with both the old and the new policy.

.. rubric:: The public

Remember that the disclosure preferences affect, which contact information
can be seen in **WHOIS and RDAP**.
