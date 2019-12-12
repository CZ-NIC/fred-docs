


Entity lookup
-----------------

This query can be used to look up a single contact by its handle.
The query cannot be used to look up a registrar.

The server does not recognize any parameters with this query.

.. code-block:: cirru
   :caption: Query path segment

   /entity/HANDLE

On the top level, the response may contain members:

* ``entities`` -- an array of entities (the :term:`designated registrar`), :rfc:`7483#section-5.1`
* ``events`` -- an array of events that have occurred on the entity, :rfc:`7483#section-4.5`
* ``handle`` -- registry-unique string identifier referencing the entity (contact handle), :rfc:`7483#section-3`
* ``links`` -- navigation to related on-line resources, :rfc:`7483#section-4.2`
* ``notices`` -- information about the service, :rfc:`7483#section-4.3`
* ``objectClassName`` -- string "entity" representing the object type in RDAP, :rfc:`7483#section-4.9`
* ``port43`` -- hostname of Registry WHOIS server, :rfc:`7483#section-4.7`
* ``rdapConformance`` -- an array of strings, each providing a hint on the used specification, :rfc:`7483#section-4.1`
* ``status`` -- an array of status flags describing the object state,
  see :doc:`StatusMap`, :rfc:`7483#section-4.6` and :rfc:`8056#section-2`
* ``vcardArray`` -- a jCard with the entity's contact information, :rfc:`7483#section-5.1`

.. code-block:: json
   :caption: Response example (https://rdap.nic.cz/entity/CZ-NIC)

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
           }
       ],
       "handle": "CZ-NIC",
       "links": [
           {
               "href": "https://rdap.nic.cz/entity/CZ-NIC",
               "type": "application/rdap+json",
               "rel": "self",
               "value": "https://rdap.nic.cz/entity/CZ-NIC"
           }
       ],
       "rdapConformance": [
           "rdap_level_0"
       ],
       "port43": "whois.nic.cz",
       "objectClassName": "entity",
       "notices": [
           {
               "description": [
                   "(c) 2015 CZ.NIC, z.s.p.o.\n\nIntended use of supplied data and information\n\nData contained in the domain name register, as well as information supplied through public information services of CZ.NIC association, are appointed only for purposes connected with Internet network administration and operation, or for the purpose of legal or other similar proceedings, in process as regards a matter connected particularly with holding and using a concrete domain name.\n"
               ],
               "title": "Disclaimer"
           }
       ],
       "vcardArray": [
           "vcard",
           [
               [
                   "version",
                   {},
                   "text",
                   "4.0"
               ],
               [
                   "fn",
                   {},
                   "text",
                   "CZ.NIC, z.s.p.o."
               ],
               [
                   "org",
                   {},
                   "text",
                   "CZ.NIC, z.s.p.o."
               ],
               [
                   "adr",
                   {
                       "type": ""
                   },
                   "text",
                   [
                       "",
                       "Milesovska 1136/5",
                       "",
                       "",
                       "Praha 3",
                       "",
                       "130 00",
                       "CZ"
                   ]
               ]
           ]
       ],
       "events": [
           {
               "eventActor": "REG-CZNIC",
               "eventAction": "registration",
               "eventDate": "2008-10-17T10:08:21+00:00"
           },
           {
               "eventAction": "last changed",
               "eventDate": "2018-05-15T19:32:00+00:00"
           }
       ]
   }
