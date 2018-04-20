:orphan:


Considerations for upgrade to FRED 2.37
=======================================

:abbr:`TBC (to be confirmed)` -- Please, wait for it.

..
   Big change in the EPP server policies because of GDPR...

   Policy changes to hide and we need to hide most of contact information that used to be shown. -> migration script

   Policies of the EPP server are still hard-coded. A detailed description can be
   found in :doc:`/EPPReference/PoliciesRules`.

   We will use the migration script (TODO link) to reset disclose flags according to these rules:

   * reversed disclosure policy of the server - hide all with the exception of name, organization, and address
   * if a contact (of a natural person) is verified or validated, hide address, too (ignoring previous setting)

