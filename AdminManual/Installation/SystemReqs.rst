
.. _system-reqs:

System requirements
-------------------

This section describes the environment suitable for running the FRED.

Hardware
^^^^^^^^

We recommend to run the FRED on **64-bit** architectures.

Binaries are available only for 64-bit architectures.

Sources can be compiled for both 32-bit and 64-bit architectures
but the 32-bit variant is no longer tested or supported.


Operating system
^^^^^^^^^^^^^^^^^

To deploy binaries, you must have installed one of these **operating systems**:

* Ubuntu 16.04 LTS (Xenial Xerus)
* Fedora 29
* Fedora 30
* Fedora 31
* RHEL 7
* CentOS 7

To compile sources from tarballs, you may try to use any Linux distribution
of your choice, but we tested the compilation/installation procedure
only on Ubuntu.


.. _system-reqs-aux:

Auxiliary software
^^^^^^^^^^^^^^^^^^

.. NOTE "large programs" that must run concurrently with the FRED

To make use of all FRED features, the following auxiliary programs are required:

* (essential) CORBA naming server (OmniNames),
* (essential) PostgreSQL database server (PG>=9.6 [#pg]_),
* (essential) Apache web server (Apache>2.2),
* mail server (Postfix, Sendmail, Exim or other),
* DNS server (KnotDNS, Bind, NSD or other).

.. Note:: All of these tools are installed automatically when installing
   from binaries but they must be installed manually when you decide to compile
   source code yourself. But don't worry, the appropriate packages
   are included in the dependency lists for each supported operating system.

.. [#pg] FRED might be able to run with PG >= 9.4, but versions lower than 9.6
   are no longer tested.

   We highly recommend to use PG 9.6 as this is the PG version we use
   for development and testing.
