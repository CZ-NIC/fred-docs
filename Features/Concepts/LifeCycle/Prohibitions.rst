
.. include:: images.subst.rst

.. _lifecycle-prohibitions:

Prohibitions
============

Prohibitions are flags which affect the basic flow of objects' life cycle
or forbid some operations on objects.

.. Note:: The prohibitions do NOT apply to the system registrar! |br|
   No matter which prohibition flags are set, the system registrar may always modify objects.

:Setting: manually
:Visible: externally

.. rubric:: Prohibition flags

:Allowed for: domains

|flag-prohibit-chown| ``serverRegistrantChangeProhibited`` |br|
The registrar may not change the :term:`domain owner` (:code:`update_domain ... <registrant> ...`).

|flag-prohibit-renew| ``serverRenewProhibited`` |br|
The registrar may not renew the domain.

:Allowed for: all registrable objects

|flag-prohibit-delete| ``serverDeleteProhibited`` |br|
The registrar may not delete the object.

|flag-prohibit-transfer| ``serverTransferProhibited`` |br|
Registrars may not transfer the object.

|flag-prohibit-update| ``serverUpdateProhibited`` |br|
The registrar may not update the object.



User blocking (locks)
---------------------

Any registrable object may be blocked as an enhanced security setting by
a contact linked to this object or the contact itself via the :term:`public request`\ s.

:Affects: EPP

.. figure:: /Features/_graphics/Lifecycle-locks.png
   :align: center

   Locks

   :doc:`Legend <index>`

* **0** :ref:`(zero state) <life-cycle-zero>` – **no blocking** |br|
  If the object has no blocking, the registrant may request to *block transfer*
  or *block all changes* (transfer and update).

* **blocked transfer** (``serverTransferProhibited`` flag) |br|
  If transfer is already blocked, the registrant may request either
  to *unblock transfer* or to *block all changes*.

* **blocked all changes** (``serverTransferProhibited`` and ``serverUpdateProhibited`` flags) |br|
  The registrant may request to *unblock all changes*.

These changes are allowed only assuming that the object does not have the flag ``serverBlocked``.

Administrative blocking
-----------------------

:Affects: EPP, expiration, obsoletion

Domains (together with the :term:`domain owner`\ s, eventually) can be blocked
by the Registry operator :ref:`via Daphne <task-admin-blocking>`,
e.g. when the registration rules or the law are being violated, or when there is
a police investigation or litigation ongoing.

When an object is blocked by the Registry operator, it has the flag ``serverBlocked``.

|flag-blocked| ``serverBlocked`` :sup:`domains, contacts` |br|
Prohibitions are set by the Registry operator and they can be revoked **only**
by the Registry operator.

To define a blocking state, any combination of the prohibition flags above can be set,
and in domains, this can even be combined with the manual zone presence flags ``serverInzoneManual``
or ``serverOutzoneManual``.

There are no restrictions on transitions from one blocking state to another.
