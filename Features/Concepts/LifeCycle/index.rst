
.. include:: images.subst.rst


Life cycle of registrable objects
=================================

This chapter describes the life cycle of :term:`registrable object`\ s
that is based on object *flags*.

A set of flags assigned to an object at a given moment constitutes an object *state*.



.. rubric:: Legend

.. _life-cycle-zero:

``0`` zero state
   any object state that does not involve any other flags from the same basic flow

arrow description
   transition originator, e.g.:

   * ``time`` – transition is based on the flow of time
   * ``EPP`` – transition caused by an EPP operation
   * ``admin`` – transition by administrative intervention

|flag-prohibit| |br|
   :doc:`prohibition(s) <Prohibitions>`

**!** ``flag``
   flag must not be set

.. toctree::
   :caption: Table of contents

   Domains
   NonDomains
   Prohibitions
   FormalRules
