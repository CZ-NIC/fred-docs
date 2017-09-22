
.. _FRED-Arch-uagents:

User agents
-------------

In general, user agents are applications in the client-server model that act
as clients and communicate with a server on behalf of a user. Most user agents
in the FRED schema, such as a web browser, are not actual components of FRED.
However, there is an exception of the EPP client which is a user agent
that comes with the FRED.

.. _FRED-Arch-uagents-epp:

EPP client
^^^^^^^^^^

The EPP client is a tool that allows registrars to register, delete and modify
objects in the Registry.

The EPP client API allows registrars to implement their own application
to access the EPP service or integrate it with their systems. The API is coded
in Python.

Also, the :program:`fred-client` command-line application is available
which is a reference implementation of the API and ready to use.

.. _FRED-Arch-uagents-whois:

Whois client
^^^^^^^^^^^^

This can be any application that can request domain information
via the WHOIS protocol (typically the command-line :program:`whois`).

.. _FRED-Arch-uagents-rdap:

RDAP client
^^^^^^^^^^^

This can be any application that can request domain information
via the REST API and process a response in the JSON format.

Web browser
^^^^^^^^^^^

A web browser is just a web browser.