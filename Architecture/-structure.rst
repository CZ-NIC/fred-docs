
.. _FRED-Arch-structure:

Publication structure (Architecture)
====================================

* Layers of the system (Central Registry/FRED/DSD-NG)

* Blackbox model
   * external interfaces
   * 3rd-party software required for operation
      * PostgreSQL, Postfix, CORBA Nameserver, Apache, DNS server...

* Top-level components
   * CR backend servers, CORBA clients (interface servers), clients
   * internal interfaces (CORBA IDL)

* Components decomposition?

* Logical data model
   * registrable objects/CR objects/all objects + relationships
   * object states, object life cycle

* Physical data model - ERD (generate from SQL?)

* Source code organization
   * mapping of components to repositories
   * (mapping of components to source files)
   * dependencies on 3rd-party libraries
   * dependencies across projects (repositories)


* All-in-one diagram? (quickref)
