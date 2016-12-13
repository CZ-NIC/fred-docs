
.. _system-reqs:

System requirements
-------------------

This section describes the environment suitable for running the FRED.

Hardware
^^^^^^^^

We recommend to run the FRED on **64-bit** architectures.

Binaries are available only for 64-bit architectures.

Sources can be compiled for both 32-bit and 64-bit architectures
but the 32-bit variant is no longer tested.


Operating system
^^^^^^^^^^^^^^^^^

To deploy binaries, you must have installed one of these **operating systems**:

* Ubuntu 12.04 LTS (Precise Pangolin) – supported only until April 2017
* Ubuntu 14.04 LTS (Trusty Tahr)
* Ubuntu 16.04 LTS (Xenial Xerus)
* Fedora 23

To compile sources from tarballs, you can use any Linux distribution of your
choice in theory but the compilation/installation procedure
was tested only on Ubuntu.

You can also compile sources from the provided RPM packages on any system
that contains the RPM Package Manager.


Auxiliary software
^^^^^^^^^^^^^^^^^^

.. NOTE "large programs" that must run concurrently with the FRED

To make use of all FRED features, the following auxiliary tools are required:

* (essential) CORBA naming server (OmniNames)
* (essential) PostgreSQL database server (PG>9),
* (essential) Apache web server (Apache>2.2),
* mail server (Postfix, Sendmail, Exim or other),
* DNS server (KnotDNS, Bind, NSD or other),

.. Note:: All of these tools are installed automatically when installing
   from binaries but they must be installed manually when you decide to compile
   the source code yourself. But don't worry, the appropriate packages
   are included in the dependency lists for each supported operating system.
