


Nameserver lookup
-----------------

This query can be used to look up a single nameserver by the :term:`FQDN`.

Lookup by IP is not implemented.

The server does not recognize any parameters with this query.

.. code-block:: cirru
   :caption: Query path segment

   /nameserver/ns.example.cz

On the top level, the response may contain members:

* ``handle`` -- registry-unique string identifier referencing the nameserver (hostname), :rfc:`7483#section-3`
* ``ldhName`` -- textual representation of DNS names, :rfc:`7483#section-3`
* ``links`` -- navigation to related on-line resources, :rfc:`7483#section-4.2`
* ``notices`` -- information about the service, :rfc:`7483#section-4.3`
* ``objectClassName`` -- string "nameserver" representing the object type in RDAP, :rfc:`7483#section-4.9`
* ``rdapConformance`` -- an array of strings, each providing a hint on the used specification, :rfc:`7483#section-4.1`

.. code-block:: json
   :caption: Response example (https://rdap.nic.cz/nameserver/a.ns.nic.cz)

   {
       "handle": "a.ns.nic.cz",
       "links": [
           {
               "href": "https://rdap.nic.cz/nameserver/a.ns.nic.cz",
               "type": "application/rdap+json",
               "rel": "self",
               "value": "https://rdap.nic.cz/nameserver/a.ns.nic.cz"
           }
       ],
       "ldhName": "a.ns.nic.cz",
       "rdapConformance": [
           "rdap_level_0"
       ],
       "notices": [
           {
               "description": [
                   "(c) 2015 CZ.NIC, z.s.p.o.\n\nIntended use of supplied data and information\n\nData contained in the domain name register, as well as information supplied through public information services of CZ.NIC association, are appointed only for purposes connected with Internet network administration and operation, or for the purpose of legal or other similar proceedings, in process as regards a matter connected particularly with holding and using a concrete domain name.\n"
               ],
               "title": "Disclaimer"
           }
       ],
       "objectClassName": "nameserver"
   }
