


Users and user interfaces
=========================

This chapter is an introduction to FRED users and user interfaces.

The end-user groups of the Registry system are:

* registrars,
* administrators,
* the public.

See also the :doc:`context diagram </Architecture/BlackboxModel>`,
which illustrates basic data flows between the users and the Registry.

.. _interfaces-rif:

Registrar interface (RIF)
-------------------------

The registrar interface enables the **registrars** to access the registry and
registrable object information, and provides them with tools to implement
operations concerning objects within the Registry. The registrars use the RIF to
send requests for the operations and receive replies from the Registry through
it.

The RIF provides the following:

* communication with registrars using the EPP protocol and secure connection,
* support for all operations concerning domains (and related :term:`registrable
  object`\ s) provided by the Registry,
* support for automatic request processing,
* connection of several registrars at the same time,
* individual account with specific access rights for each registrar,
* :doc:`logging <AuditLog>` of all communication with registrars -- each request
  is logged with a registrar identifier and a :ref:`transaction identifier
  <trans-ident>`,
* support for hiding contact information.

.. _system-registrar:

.. rubric:: System registrar

This is a registrar account that belongs to the Registry itself and allows
the Registry to edit :term:`registrable object`\ s as necessary. Normal rules
do not apply -- it can edit any object in any state (and without being designated
to manage the object), it does not need to have credit, and it does not generate
EPP notifications.

.. Important:: The system registrar account must always exist in the Registry
   database and there must be exactly one of this kind!

   See :ref:`FRED-Admin-reginit-reg` during registry initialization.

.. _interfaces-adif:

Administrator interface (ADIF)
------------------------------

The administrator interface provides **administrators** (such as customer
support workers) with tools for displaying and handling of information
in the Registry and tools for manual intervention.

The basic function of the ADIF is search in Registry records
(registrars, :term:`registrable object`\ s, logs, communications),
display of their details and manual editing thereof.
The interface allows composition of complex search queries by any record attribute
and using logical operators, limiting and sorting results, and even their export.
Users may examine historical values and their period of validity.

Editing abilities can be used for managing registrars, blocking domains
(e.g. during legal disputes or in case of law or rule breakage),
or forcing their inclusion in (or exclusion from) a zone.

Access rights are configured per user, who can be given read-only or read-write
permissions for various record types, depending on requirements of their job.

All user activity is :doc:`logged <AuditLog>` to ensure security of sensitive data.

The ADIF is mainly a Web service (WebAdmin/Daphne), which is friendly
to non-tech users. But there are also CLI programs to support some other
administrative operations, which are not available in the Web service itself,
including automated self-administration tasks.

The Registry staff may also edit domains and the other :term:`registrable object`\
s for various administrative reasons, but they must use the RIF
with the *system registrar* account.

.. _interfaces-pif:

Public interface (PIF)
----------------------

The public interface provides the **public** with public information about
domains and other :term:`registrable object`\ s recorded in the Registry.

The PIF has 3 services which provide the public information in various formats
via various protocols: Unix WHOIS service, Web WHOIS service, and RDAP service.
The Web WHOIS allows visitors to download the public information as a signed
PDF statement, too.

In addition to these services, the Registry provides a website listing accredited
registrars, which can be used by potential domain holders to pick a suitable
registrar, and *public request* forms.

.. _public-requests:

.. rubric:: Public requests

Public requests are a set of public websites which allow authorized stakeholders
to send requests to the Registry directly, whether it is for authinfo,
object (un)locking, or an overview of recorded personal information.

If the stakeholder requires information for a registered contact,
the request is authorized automatically and resolved immediately.
If the stakeholder requires information for an unregistered contact,
they must prove that they are authorized for this request
by sending either an electronically-signed email or a letter containing a notarized signature.
The authorization is checked by Registry staff and the request is resolved manually.
