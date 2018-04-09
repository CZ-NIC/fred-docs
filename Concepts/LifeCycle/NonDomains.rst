
.. include:: images.subst.rst



Non-domains obsoletion
----------------------

Non-domains are contacts, nssets, or keysets.

The life cycle of these objects is influenced mainly by their usage in EPP operations,
and :doc:`prohibitions <Prohibitions>` eventually.

:Setting: automatically
:Visible: externally
:Allowed for: contacts, nssets, keysets
:Affects: existence

.. figure:: /Concepts/_graphics/Lifecycle-nondomains.png
   :align: center

   Non-domains obsoletion

   :doc:`Legend <index>`

.. rubric:: Basic flow

* **linked** |br|
  As long as an object is assigned to another object (also is flagged ``linked``),
  it cannot become obsolete. |br|
  When an unlinked object is linked again, the protection period is "reset".

* **0** :ref:`(zero state) <life-cycle-zero>` |br|
  Once the object is unlinked, it can become obsolete. |br|
  This is the moment when the protection period starts running.

* **deleteCandidate** |br|
  When the object has been left idle (unlinked and not modified) for the whole protection period of
  :abbr:`2 (object_registration_protection_period)` months (:ref:`configurable <config-dbparams>`),
  then the ``deleteCandidate`` flag is set, unless there is :doc:`delete prohibition
  <Prohibitions>` on the object. |br|
  If set, the Registry is allowed to delete the object.

.. rubric:: Prohibitions

:doc:`Delete prohibition <Prohibitions>` prevents the Registry from setting
the ``deleteCandidate`` flag on the object and consequently deleting the object,
until the delete prohibition is revoked.

.. rubric:: Formal rules

See :ref:`rules-obsol`.
