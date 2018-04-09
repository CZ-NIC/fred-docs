
.. include:: images.subst.rst



Domains
=======

The life cycle of a domain is influenced by `registration expiration`_, :ref:`validation expiration
<validation-expiration>` (in ENUM domains), and eventually by forced :ref:`presence in a zone
<zone-presence>` (in or out) and :doc:`prohibitions <Prohibitions>`.

Registration expiration
-----------------------

This section describes a flow of states related to domain registration expiration.

:Setting: automatically
:Visible: internally or externally
:Allowed for: domains
:Affects: `zone presence`_, existence

.. figure:: /Concepts/_graphics/Lifecycle-domains-exp.png
   :align: center

   Domain registration expiration

   :doc:`Legend <index>`

.. rubric:: Basic flow

* **0** :ref:`(zero state) <life-cycle-zero>` |br|
  When a domain is freshly registered or renewed, none of the flags is on.

* **expW** (internal) |br|
  When the expiration date is approaching,
  :abbr:`30 (expiration_notify_period)` days (:ref:`configurable <config-dbparams>`) before expiration,
  the ``expirationWarning`` flag is set, which may trigger a notification.

* **expired** |br|
  When the actual expiration date arrives, the ``expired`` flag is set, which may trigger a notification. |br|
  However, the domain is still generated to the zone for some time.

* **ouW** (internal) |br|
  :abbr:`25 (outzone_unguarded_email_warning_period)` days (:ref:`configurable <config-dbparams>`) after expiration,
  the ``outzoneUnguardedWarning`` flag is set, which may trigger a notification.

* **unguarded** |br|
  :abbr:`30 (expiration_dns_protection_period)` days (:ref:`configurable <config-dbparams>`) after expiration,
  the domain becomes ``unguarded`` (and is flagged so), which results in exclusion from the zone (flagged also ``outzoneUnguarded``).

* **delW** (internal) |br|
  :abbr:`34 (expiration_letter_warning_period)` days (:ref:`configurable <config-dbparams>`) after expiration,
  the ``deletionWarning`` flag is set, which may trigger a notification.

* **deleteCandidate** |br|
  :abbr:`61 (expiration_registration_protection_period)` days (:ref:`configurable <config-dbparams>`) after expiration,
  the ``deleteCandidate`` flag is set, unless there is :doc:`delete prohibition <Prohibitions>` on the domain.
  If set, the domain cannot be renewed anymore and the Registry is allowed to delete the domain.

The flags accumulate. (Each state includes flags of the preceding state,
e.g. when a domain has the ``expired`` flag, it also has the ``expirationWarning``
flag.)

The flags are unset when the domain is renewed.

.. rubric:: Prohibitions

Setting of the :doc:`renew prohibition <Prohibitions>` will cause the domain
to be taken out of the basic flow (none of those flags will be set).
The expiration flags are, however, returned to the domain (re-calculated
according to the current date), once the renew prohibition has been revoked.

:doc:`Delete prohibition <Prohibitions>` prevents the Registry from setting
the ``deleteCandidate`` flag on the domain and consequently deleting the domain,
until the delete prohibition is revoked.

.. rubric:: Zone-inclusion according to registration states

.. list-table::
   :widths: 16 12 12 12 12 12 12 12
   :header-rows: 1

   * - State
     - 0
     - expW
     - expired
     - ouW
     - unguarded
     - delW
     - delCandidate
   * - Allows inclusion
     - Yes
     - Yes
     - Yes
     - Yes
     - No
     - No
     - No

.. rubric:: Formal rules

See :ref:`rules-regex`.


.. _validation-expiration:

Validation expiration
---------------------

This section describes a flow of states related to ENUM domain validation expiration.

:Setting: automatically
:Visible: internally or externally
:Allowed for: :term:`ENUM` domains
:Affects: `zone presence`_

.. figure:: /Concepts/_graphics/Lifecycle-domains-val.png
   :align: center

   ENUM domain validation expiration

   :doc:`Legend <index>`

.. rubric:: Basic flow

* **0** :ref:`(zero state) <life-cycle-zero>` |br|
  When a domain is freshly registered or its validation expiration date renewed/updated,
  none of the flags is on.

* **valW1** (internal) |br|
  When the validation expiration date is approaching,
  :abbr:`30 (validation_notify1_period)` days (:ref:`configurable <config-db>`) before validation expiration,
  ``validationWarning1`` flag is set, which may trigger the 1st warning notification.

* **valW2** (internal) |br|
  When the validation expiration date is approaching,
  :abbr:`15 (validation_notify2_period)` days (:ref:`configurable <config-db>`) before validation expiration,
  ``validationWarning2`` flag is set, which may trigger the 2nd warning notification.

* **notValidated** |br|
  When the actual validation expiration date comes, ``notValidated`` flag is set,
  which results in the domain not being generated to the zone anymore.

The flags accumulate. (Each state includes flags of the preceding state,
e.g. when a domain has the ``notValidated`` flag, it also has the
``validationWarning1`` and ``validationWarning2`` flags.)

The flags are unset when the validation is renewed/updated.

.. rubric:: Prohibitions

Prohibitions do not affect this flow.

.. rubric:: Zone-inclusion according to validation states

.. list-table::
   :widths: 30 12 12 12 12
   :header-rows: 1

   * - State
     - 0
     - valW1
     - valW2
     - notVal
   * - Allows inclusion
     - Yes
     - Yes
     - Yes
     - No

.. rubric:: Formal rules

See :ref:`rules-valex`.

.. _zone-presence:

Zone presence
-------------

There are two ways to determine whether a domain shall be generated to a zone.

The domain is naturally included in the zone if and only if it meets the following conditions:

* the domain is not ``unguarded``, and
* the domain is validated if it is an ENUM domain, and
* the domain has a nsset assigned to it, and
* the domain is not forced out of the zone manually, i.e. it does not have the ``serverOutzoneManual`` flag. |br|
  This flag forces the domain not to be included despite having met the conditions above.

The domain can be forced to the zone by setting the manual flag ``serverInzoneManual``.
This can override registration expiration flow up to ``deleteCandidate`` and expired validation.
However, if the domain does not have a nsset, this flag will not have the desired effect.

Neither of these manual flags affects the basic flow.

When the domain is not generated to the zone for *any reason*, it is indicated
with the ``outzone`` flag.
