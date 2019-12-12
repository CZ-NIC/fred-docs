
Keyset lookup
-----------------

This query can be used to look up a single keyset by its handle.

The server does not recognize any parameters with this query.

.. code-block:: cirru
   :caption: Query path segment

   /fred_keyset/HANDLE

On the top level, the response may contain members:

* ``dns_keys`` -- an array of keyData objects defined as a part of the Domain object class, :rfc:`7483#section-5.3`
* ``entities`` -- an array of entities (linked contacts and the :term:`designated registrar`), :rfc:`7483#section-5.1`
* ``events`` -- an array of events that have occurred on the keyset, :rfc:`7483#section-4.5`
* ``handle`` -- registry-unique string identifier referencing the keyset, :rfc:`7483#section-3`
* ``links`` -- navigation to related on-line resources, :rfc:`7483#section-4.2`
* ``notices`` -- information about the service, :rfc:`7483#section-4.3`
* ``objectClassName`` -- string "fred_keyset" representing the object type in RDAP, :rfc:`7483#section-4.9`
* ``port43`` -- hostname of Registry WHOIS server, :rfc:`7483#section-4.7`
* ``rdapConformance`` -- an array of strings, each providing a hint on the used specification, :rfc:`7483#section-4.1`
* ``status`` -- an array of status flags describing the object state,
  see :doc:`StatusMap`, :rfc:`7483#section-4.6` and :rfc:`8056#section-2`

.. code-block:: json
   :caption: Response example (https://rdap.nic.cz/fred_keyset/CZ.NIC)

   {
       "status": [
           "associated"
       ],
       "handle": "CZ.NIC",
       "links": [
           {
               "href": "https://rdap.nic.cz/fred_keyset/CZ.NIC",
               "type": "application/rdap+json",
               "rel": "self",
               "value": "https://rdap.nic.cz/fred_keyset/CZ.NIC"
           }
       ],
       "port43": "whois.nic.cz",
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
       "dns_keys": [
           {
               "protocol": 3,
               "flags": 257,
               "algorithm": 5,
               "publicKey": "BQEAAAABt3LenoCVTV0okqKYPDnnVJqvwCD9MKJNXg8fcOCdLQYncyoehpwM5RK2UkZDcDxWkMo7yMa35ej+Mhpaji9si4xXD+Syl4Q06LFiFkdN/5GlVlrIdE3GW7zC7Z4sS14Vz8FbYfcRmhsh19Ob718jGZneGfw2UPbvkyxUR8wD7mguZn02fQ6tjj/Ktp4uSW9tpz3bjGMo2rX+iZk4xgbPaesAOlR/AaHdatGZsWC9CPon8mnLZeu6czm8CBDgBmnf3PE8c5+uyWj1Pw4pp0VQmnX5UrnuGpErg7qXhJm7wY2CRVRMcLX3zmjVWXW1uT9JFh2G+/pZzxnASfKKltZpuw=="
           }
       ],
       "rdapConformance": [
           "rdap_level_0",
           "fred_version_0"
       ],
       "notices": [
           {
               "description": [
                   "(c) 2015 CZ.NIC, z.s.p.o.\n\nIntended use of supplied data and information\n\nData contained in the domain name register, as well as information supplied through public information services of CZ.NIC association, are appointed only for purposes connected with Internet network administration and operation, or for the purpose of legal or other similar proceedings, in process as regards a matter connected particularly with holding and using a concrete domain name.\n"
               ],
               "title": "Disclaimer"
           }
       ],
       "objectClassName": "fred_keyset",
       "events": [
           {
               "eventAction": "registration",
               "eventDate": "2009-01-21T14:12:26+00:00"
           },
           {
               "eventAction": "last changed",
               "eventDate": "2013-09-20T09:18:37+00:00"
           }
       ]
   }
