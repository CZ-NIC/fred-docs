


Listing
===============

Commands for object listing.

Object listing is done in two steps that are performed separately in this order:

#. Request for the listing of objects – objects are selected and prepared
   on the server, the client receives only the count of prepared objects,
#. Get results – handles of the prepared objects are delivered to the client.

..
   Simple commands: ``<fred:listDomains/>``, ``<fred:listContacts/>``, ``<fred:listNssets/>``,
   ``<fred:listKeysets/>``, ``<fred:getResults/>``

   Parametrized commands: ``<fred:domainsByContact>``, ``<fred:domainsByNsset>``,
   ``<fred:domainsByKeyset>``, ``<fred:nssetsByContact>``,
   ``<fred:keysetsByContact>``, ``<fred:nssetsByNs>``

.. toctree::
   :maxdepth: 1

   Prepare
   GetResults
