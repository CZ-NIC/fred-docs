


Whois & RDAP
------------

There are two versions of the WHOIS service.

The first version is a classical Unix WHOIS service as specified in :rfc:`1834`.
This service features recursive results for all associated objects
and inverse queries.

The second version is a `web WHOIS application <https://www.nic.cz/whois/>`_.
The web version supports hyperlinked and more detailed results.
There is even a possibility to enable CAPTCHA protection against robots.

Both versions contain the security feature of hiding personal data of contacts.

Additionally, the FRED contains a prototype implementation of the RDAP protocol
which allows client applications to obtain results in a more recent,
machine-readable format (JSON).
