


Managed objects
===============

The FRED EPP uses custom representations of registrable objects:

* domain (regular or ENUM),
* contact,
* nsset = a set of name servers,
* keyset = a set of DNSSEC keys.

Each registrable object is defined by its associated attributes that can be
viewed and modified by the client (the :term:`designated registrar`) or the server,
and by command-response mapping.

Attribute values are defined by the data types of schemas (syntax, that is
allowed characters, length, pattern),
and sometimes additional constraints that are described in this chapter.

Custom managed objects are object-level extensions of EPP which appear
in these XPaths:

* standard commands: :samp:`/epp/command/{$std-cmd}/{$object}:{$std-cmd}`
* extending commands: :samp:`/epp/extension/fred:extcommand/fred:{$ext-cmd}/{$object}:{$ext-cmd}`

Substitutions used in the paths:

*$std-cmd* can be a name of a standard object-related command, such as ``create``, |br|
*$ext-cmd* can be a name of an extending object-related command, such as ``sendAuthInfo``, |br|
*$object* is a prefix for an object namespace.

.. rubric:: Chapter TOC

.. toctree::

   Common
   Domains
   Contacts
   Nssets
   Keysets
