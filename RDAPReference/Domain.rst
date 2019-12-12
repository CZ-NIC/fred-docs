


Domain lookup
-------------

This query can be used to look up a single domain by the :term:`FQDN` in a zone administered by the Registry.

Lookup by IP is not implemented.

The server does not recognize any parameters with this query.

.. code-block:: cirru
   :caption: Query path segment

   /domain/example.cz

On the top level, the response may contain members:

* ``entities`` -- an array of entities (linked contacts and the :term:`designated registrar`), :rfc:`7483#section-5.1`
* ``events`` -- an array of events that have occurred on the domain, :rfc:`7483#section-4.5`
* ``fred_keyset`` -- linked keyset (FRED extension), see :doc:`FRED_keyset` for members
* ``fred_nsset`` -- linked nsset (FRED extension), see :doc:`FRED_nsset` for members
* ``handle`` -- registry-unique string identifier referencing the domain (domain name), :rfc:`7483#section-3`
* ``ldhName`` -- textual representation of DNS names, :rfc:`7483#section-3`
* ``links`` -- navigation to related on-line resources, :rfc:`7483#section-4.2`
* ``nameservers`` -- an array of :doc:`nameserver objects <Nameserver>`, :rfc:`7483#section-5.2`
* ``notices`` -- information about the service, :rfc:`7483#section-4.3`
* ``objectClassName`` -- string "domain" representing the object type in RDAP, :rfc:`7483#section-4.9`
* ``port43`` -- hostname of Registry WHOIS server, :rfc:`7483#section-4.7`
* ``rdapConformance`` -- an array of strings, each providing a hint on the used specification, :rfc:`7483#section-4.1`
* ``secureDNS`` -- secure DNS information, :rfc:`7483#section-5.3`
* ``status`` -- an array of status flags describing the object state,
  see :doc:`StatusMap`, :rfc:`7483#section-4.6` and :rfc:`8056#section-2`

.. Note:: A response may contain an ``actionEvent`` called "enum validation expiration",
   which is an extension of events in ENUM domains.
   See `specification <https://fred.nic.cz/rdap-extension/#ext-responses-enum>`_.

   .. code-block:: json
      :caption: Example of additional event in an ENUM domain

      {
         "handle": "1.2.3.4.5.6.7.8.9.0.2.4.e164.arpa",
         "...",
         "events": [
            "...",
            {
               "eventAction": "enum validation expiration",
               "eventDate": "2018-09-15T14:00:00+00:00"
            },
            "...",
         ]
      }

.. code-block:: json
   :caption: Response example (https://rdap.nic.cz/domain/nic.cz)

   {
      "fred_nsset": {
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
         "objectClassName": "fred_nsset",
         "handle": "CZ.NIC",
         "links": [
            {
               "href": "https://rdap.nic.cz/fred_nsset/CZ.NIC",
               "type": "application/rdap+json",
               "rel": "self",
               "value": "https://rdap.nic.cz/fred_nsset/CZ.NIC"
            }
         ]
      },
      "handle": "nic.cz",
      "links": [
         {
            "href": "https://rdap.nic.cz/domain/nic.cz",
            "type": "application/rdap+json",
            "rel": "self",
            "value": "https://rdap.nic.cz/domain/nic.cz"
         }
      ],
      "port43": "whois.nic.cz",
      "fred_keyset": {
         "objectClassName": "fred_keyset",
         "handle": "CZNIC",
         "links": [
            {
               "href": "https://rdap.nic.cz/fred_keyset/CZNIC",
               "type": "application/rdap+json",
               "rel": "self",
               "value": "https://rdap.nic.cz/fred_keyset/CZNIC"
            }
         ],
         "dns_keys": [
            {
               "protocol": 3,
               "flags": 257,
               "algorithm": 13,
               "publicKey": "LM4zvjUgZi2XZKsYooDE0HFYGfWp242fKB+O8sLsuox8S6MJTowY8lBDjZD7JKbmaNot3+1H8zU9TrDzWmmHwQ=="
            }
         ]
      },
      "secureDNS": {
         "keyData": [
            {
               "protocol": 3,
               "flags": 257,
               "algorithm": 13,
               "publicKey": "LM4zvjUgZi2XZKsYooDE0HFYGfWp242fKB+O8sLsuox8S6MJTowY8lBDjZD7JKbmaNot3+1H8zU9TrDzWmmHwQ=="
            }
         ],
         "zoneSigned": true,
         "maxSigLife": 1209600,
         "delegationSigned": true
      },
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
      "ldhName": "nic.cz",
      "entities": [
         {
            "objectClassName": "entity",
            "handle": "CZ-NIC",
            "links": [
               {
                  "href": "https://rdap.nic.cz/entity/CZ-NIC",
                  "type": "application/rdap+json",
                  "rel": "self",
                  "value": "https://rdap.nic.cz/entity/CZ-NIC"
               }
            ],
            "roles": [
               "registrant"
            ]
         },
         {
            "objectClassName": "entity",
            "handle": "REG-CZNIC",
            "roles": [
               "registrar"
            ]
         },
         {
            "objectClassName": "entity",
            "handle": "FEELA",
            "links": [
               {
                  "href": "https://rdap.nic.cz/entity/FEELA",
                  "type": "application/rdap+json",
                  "rel": "self",
                  "value": "https://rdap.nic.cz/entity/FEELA"
               }
            ],
            "roles": [
               "administrative"
            ]
         },
         {
            "objectClassName": "entity",
            "handle": "MAPET",
            "links": [
               {
                  "href": "https://rdap.nic.cz/entity/MAPET",
                  "type": "application/rdap+json",
                  "rel": "self",
                  "value": "https://rdap.nic.cz/entity/MAPET"
               }
            ],
            "roles": [
               "administrative"
            ]
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
      "objectClassName": "domain",
      "events": [
         {
            "eventAction": "registration",
            "eventDate": "1997-10-30T00:00:00+00:00"
         },
         {
            "eventAction": "expiration",
            "eventDate": "2027-03-15T13:00:00+00:00"
         },
         {
            "eventAction": "last changed",
            "eventDate": "2016-11-22T14:07:40+00:00"
         },
         {
            "eventAction": "transfer",
            "eventDate": "2007-02-28T13:55:00+00:00"
         }
      ],
      "status": [
         "active"
      ],
   }
