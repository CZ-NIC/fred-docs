
.. _system-reqs:

System requirements
-------------------

This section describes the environment suitable for running the FRED.

.. only:: mode_structure

   .. todo:: CHECK system requirements

Hardware
^^^^^^^^

We recommend to run the FRED on **64-bit** architectures.



Operating system
^^^^^^^^^^^^^^^^^

To deploy binaries, you must have installed one of these **operating systems**:

* Ubuntu 12.04 LTS (Precise Pangolin)
* Ubuntu 14.04 LTS (Trusty Tahr)
* Ubuntu 16.04 LTS (Xenial Xerus)
* Fedora 23


.. only:: mode_structure

   .. todo:: To install FRED from source code, ... ???

      * can be compiled for 32-bit archs? is it worth mentioning?
      * other linux distributions?



Auxiliary software
^^^^^^^^^^^^^^^^^^

To make use of all FRED features, the following auxiliary tools are required:

* CORBA naming server (OmniNames)
* database server (PostgreSQL),
* mail server (Postfix),
* DNS server (bind),
* web server (Apache)

.. only:: mode_structure

   .. todo:: xsltproc, ... ?

.. Note:: All of these tools are installed automatically when installing
   from binaries but they must be installed manually when you decide to compile
   the source code yourself. But don't worry, the appropriate packages
   are included in the dependency lists for each supported operating system.
