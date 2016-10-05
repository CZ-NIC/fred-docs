


Registry–Registrar–Registrant model
-----------------------------------

The most important feature of the FRED is its database structured according 
to the Registry–Registrar–Registrant model. Registrars communicate 
with the Registry on behalf of Registrants (domain owners). 
Strong ownership model ensures that each registrable object in the database 
is owned by one Registrar and no other Registrar can modify it. 
A Registrant is allowed to change their Registrar by means of a transfer 
process.

The registrable objects are the following:

* Domain,
* Contact (in roles of domain owners, administrative contacts 
  or technical contacts),
* NSSet (a group of name servers), and
* KeySet (a group of DNSSEC keys).

All registration requests are resolved immediately if the requested object 
is free. 

The history of all changes regarding any object is accessible 
through an administration interface. 
