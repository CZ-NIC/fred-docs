
Permissions
===========

Permissions are managed through the Django admin site, which is
separate from the main Ferda user interface, and can be accessed on the
:file:`/admin` path.

A user with access to the admin site must be given the *Staff status*
and can be designated to have all permissions implicitly with the *Superuser
status*.

User management permissions:

- ``Can view user``
- ``Can add user``
- ``Can change user``
- ``Can delete user``

Registry management permissions:

- ``Can view basic registry content`` -- required to display any information
  from the Registry
- ``Can view AuthInfo`` -- required to display the transfer password
- ``Can view registrar credit``

You may create groups of these permissions and assign them to users.

Users and groups example
------------------------

This example describes a model situation where we have two groups
of permissions: one for customer support team workers and another for customer
support team managers.

Groups

- a *Customer Support Lead* group might have all Registry management permissions
- a *Customer Support Worker* group might have only the permission
  ``Can view basic registry content``

Users

- users of customer support who require only basic permissions would be
  assigned the *Customer Support Worker* group
- a user of a customer support manager who requires extended permissions,
  would be assigned the *Customer Support Lead* group
