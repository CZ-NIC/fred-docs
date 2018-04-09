


Automatic keyset management
===========================

AKM is based on the two RFCs:

* :rfc:`7344` Automating DNSSEC Delegation Trust Maintenance,
* :rfc:`8078` Managing DS Records from the Parent via CDS/CDNSKEY.

Domains are included in the :term:`AKM` strictly
on demand when they publish valid CDNSKEY resource records [*]_ on domains' name servers.
Registrants are supposed to ask their DNS operators to do so or not to do so.

.. Tip::

   The KnotDNS can be easily configured to support `automatic key management
   <https://www.knot-dns.cz/docs/2.6/html/configuration.html#automatic-dnssec-signing>`_.

A CDNSKEY contains the KSK of a child zone (domain) solely for the purpose to request
updates to DS records in the parent zone (Registry). DS records are calculated
by the Registry; see also :doc:`zone generation concept </Concepts/Genzone>`.

The CDNSKEY resource records are recognized by the FRED as **valid** when they comply
with the same constraints as the rest of managed keysets – see
:ref:`keyset attributes in the EPP Reference Manual <mng-keyset-attr>`.

A special case is the "delete key" (``CDNSKEY 0 3 0 AA==``) which can be
published to request removal of a domain from AKM.

.. [*] The FRED does not support CDS resource records.

Security status cases
---------------------

The Registry handles the request for update according to the security status of a domain:

* an insecured domain (registered without a keyset) requests to be included in AKM,
* a domain secured with a manually-managed keyset requests to be switched to AKM,
* a domain secured with an auto-managed keyset requests to update the keys.

Acceptance of new keys
----------------------

When introducing a new domain in AKM, the Registry handles differently domains
which do not register yet as DNSSEC-enabled (without a keyset, insecured)
and those that are secured with a keyset:

* When a domain is already secured with a keyset, adoption of new keys happens
  immediately because the new keys can be authenticated using the old keys,
  and the domain is switched to AKM.

* When a domain is not secured yet, the detected keys must undergo the **acceptance
  period** during which they must remain valid and unchanged on all name servers
  in the associated nsset.
  The acceptance period acts as a security measure instead of key authentication.
  After the keys pass the acceptance period successfully, then they are adopted
  and the domain is switched to AKM.

The **acceptance period** is initiated when valid CDNSKEY resource records are found
for the first time during a scan. In subsequent scans, the records must be found
again in exactly the same state and on all the name servers as before, otherwise
the acceptance period is broken and the whole process must be restarted.

Management task
---------------

The task of keyset management is performed in several steps:

#. Loads selected domains and all name servers of insecured domains
   from their nssets, and sorts them in the scan queue.
#. Scans domains in the scan queue:

   - if a domain is insecured, name servers are asked by the scanner directly
     via TCP queries whether they have CDNSKEY records for domains,
   - if a domain is secured, the CDNSKEY records are requested via a local resolver
     and a response is validated with DNSSEC inside the scanner,

   and saves the results.

#. Notifies technical contacts of the nssets about the initiated or broken
   acceptance period (insecure domains only).
#. Updates keys:

   - applies new keys if they have passed the acceptance period
     (EPP operations create_keyset & update_domain),
   - switches domains to AKM if they have been secured and they have requested
     AKM (EPP operations create_keyset & update_domain),
   - updates auto-managed keysets (AKM keyset update operation) and notifies
     technical contacts of nssets,
   - removes auto-managed keysets where removal from AKM has been requested
     (EPP operation update_domain).

See also the :ref:`AKM periodic task <cronjob-akm>`.

Components
----------

The AKM subsystem includes three components: :ref:`fred-akmd <FRED-Arch-servers-akmd>`,
:ref:`fred-akm <FRED-Arch-clients-akm>` and :ref:`cdnskey-scanner
<FRED-Arch-clients-cdnskeyscanner>`.
See also the :doc:`overall architecture </Architecture/TopLevelComponents/index>`
for component relations.

Notifications
-------------

The AKM task triggers the following notifications:

* Initiated acceptance period – :ref:`email-type-akm-ok`
* Broken acceptance period – :ref:`email-type-akm-ko`
* Update of auto-managed keys – :ref:`email-type-akm-upd`

The utilized EPP operations (create_keyset, update_domain) trigger additional
notifications of their own:

*  :ref:`email-type-notify-create` and/or
* :ref:`email-type-notify-update` and :ref:`EPP poll message type: Object update <epp-poll-type-update>`.
