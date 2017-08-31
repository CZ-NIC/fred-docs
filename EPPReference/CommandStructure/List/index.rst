


Listing
===============

Commands for object listing.

Object listing is done in two steps which are performed separately in this order:

#. Prepare a list – objects are selected and prepared
   on the server, the client receives only the count of prepared objects,
#. Get results – a chunk of handles of the prepared objects is delivered to the client.
   This command must be repeated to retrieve the remaining chunks
   until it returns an empty results list.

The list of objects remaining on the server is retained between sessions.

Calling another list preparation resets the list of unretrieved results on the server!

..
   Simple commands: ``<fred:listDomains/>``, ``<fred:listContacts/>``, ``<fred:listNssets/>``,
   ``<fred:listKeysets/>``, ``<fred:getResults/>``

   Parametrized commands: ``<fred:domainsByContact>``, ``<fred:domainsByNsset>``,
   ``<fred:domainsByKeyset>``, ``<fred:nssetsByContact>``,
   ``<fred:keysetsByContact>``, ``<fred:nssetsByNs>``

.. toctree::

   Prepare
   GetResults
