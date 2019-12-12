
Nsset lookup
-----------------

This query can be used to look up a single nsset by its handle.

The server does not recognize any parameters with this query.

.. code-block:: cirru
   :caption: Query path segment

   /fred_nsset/HANDLE

On the top level, the response may contain members:

* ``entities`` -- an array of entities (linked contacts and the :term:`designated registrar`), :rfc:`7483#section-5.1`
* ``events`` -- an array of events that have occurred on the nsset, :rfc:`7483#section-4.5`
* ``handle`` -- registry-unique string identifier referencing the nsset, :rfc:`7483#section-3`
* ``links`` -- navigation to related on-line resources, :rfc:`7483#section-4.2`
* ``nameservers`` -- an array of :doc:`nameserver objects <Nameserver>`, :rfc:`7483#section-5.2`
* ``notices`` -- information about the service, :rfc:`7483#section-4.3`
* ``objectClassName`` -- string "fred_nsset" representing the object type in RDAP, :rfc:`7483#section-4.9`
* ``port43`` -- hostname of Registry WHOIS server, :rfc:`7483#section-4.7`
* ``rdapConformance`` -- an array of strings, each providing a hint on the used specification, :rfc:`7483#section-4.1`
* ``status`` -- an array of status flags describing the object state,
  see :doc:`StatusMap`, :rfc:`7483#section-4.6` and :rfc:`8056#section-2`

.. code-block:: json
   :caption: Response example (https://rdap.nic.cz/fred_nsset/CZ.NIC)

   {
       "status": [
           "associated"
       ],
       "entities": [
           {
               "objectClassName": "entity",
               "handle": "REG-CZNIC",
               "roles": [
                   "registrar"
               ]
           },
           {
               "objectClassName": "entity",
               "handle": "JAROMIR-TALIR",
               "links": [
                   {
                       "href": "https://rdap.nic.cz/entity/JAROMIR-TALIR",
                       "type": "application/rdap+json",
                       "rel": "self",
                       "value": "https://rdap.nic.cz/entity/JAROMIR-TALIR"
                   }
               ],
               "roles": [
                   "technical"
               ]
           },
           {
               "objectClassName": "entity",
               "handle": "JTALIR",
               "links": [
                   {
                       "href": "https://rdap.nic.cz/entity/JTALIR",
                       "type": "application/rdap+json",
                       "rel": "self",
                       "value": "https://rdap.nic.cz/entity/JTALIR"
                   }
               ],
               "roles": [
                   "technical"
               ]
           }
       ],
       "handle": "CZ.NIC",
       "links": [
           {
               "href": "https://rdap.nic.cz/fred_nsset/CZ.NIC",
               "type": "application/rdap+json",
               "rel": "self",
               "value": "https://rdap.nic.cz/fred_nsset/CZ.NIC"
           }
       ],
       "rdapConformance": [
           "rdap_level_0",
           "fred_version_0"
       ],
       "port43": "whois.nic.cz",
       "objectClassName": "fred_nsset",
       "nameservers": [
           {
               "ipAddresses": {
                   "v4": [
                       "194.0.12.1"
                   ],
                   "v6": [
                       "2001:678:f::1"
                   ]
               },
               "objectClassName": "nameserver",
               "handle": "a.ns.nic.cz",
               "links": [
                   {
                       "href": "https://rdap.nic.cz/nameserver/a.ns.nic.cz",
                       "type": "application/rdap+json",
                       "rel": "self",
                       "value": "https://rdap.nic.cz/nameserver/a.ns.nic.cz"
                   }
               ],
               "ldhName": "a.ns.nic.cz"
           },
           {
               "ipAddresses": {
                   "v4": [
                       "194.0.13.1"
                   ],
                   "v6": [
                       "2001:678:10::1"
                   ]
               },
               "objectClassName": "nameserver",
               "handle": "b.ns.nic.cz",
               "links": [
                   {
                       "href": "https://rdap.nic.cz/nameserver/b.ns.nic.cz",
                       "type": "application/rdap+json",
                       "rel": "self",
                       "value": "https://rdap.nic.cz/nameserver/b.ns.nic.cz"
                   }
               ],
               "ldhName": "b.ns.nic.cz"
           },
           {
               "ipAddresses": {
                   "v4": [
                       "193.29.206.1"
                   ],
                   "v6": [
                       "2001:678:1::1"
                   ]
               },
               "objectClassName": "nameserver",
               "handle": "d.ns.nic.cz",
               "links": [
                   {
                       "href": "https://rdap.nic.cz/nameserver/d.ns.nic.cz",
                       "type": "application/rdap+json",
                       "rel": "self",
                       "value": "https://rdap.nic.cz/nameserver/d.ns.nic.cz"
                   }
               ],
               "ldhName": "d.ns.nic.cz"
           }
       ],
       "events": [
           {
               "eventAction": "registration",
               "eventDate": "2008-06-09T12:30:16+00:00"
           },
           {
               "eventAction": "last changed",
               "eventDate": "2013-09-20T09:18:20+00:00"
           }
       ],
       "notices": [
           {
               "description": [
                   "(c) 2015 CZ.NIC, z.s.p.o.\n\nIntended use of supplied data and information\n\nData contained in the domain name register, as well as information supplied through public information services of CZ.NIC association, are appointed only for purposes connected with Internet network administration and operation, or for the purpose of legal or other similar proceedings, in process as regards a matter connected particularly with holding and using a concrete domain name.\n"
               ],
               "title": "Disclaimer"
           }
       ]
   }
