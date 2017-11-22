


FRED command & response extensions
==================================

Extensions of standard commands and responses allow to manage additional attributes
for some managed objects by including them in transactions where appropriate.

Currently, these extensions are used in transactions of :ref:`ENUM domains
<mng-domain-ext>` and :ref:`contacts with an additional mailing address
<mng-contact-ext>`.

.. _command-ext:

Command extensions
~~~~~~~~~~~~~~~~~~

Command extensions are extensions in the XPath :samp:`/epp/command/extension/*:*`.

According to the general requirements of the standard, the ``<extension>``
element is optional but if used then it must contain a sequence of one or more
elements (any namespace). The FRED EPP server requires the ``<extension>``
element to have a single child at most.

These extensions are used with the following commands:

* :doc:`domain:create </EPPReference/CommandStructure/Create/CreateDomain>`,
* :doc:`domain:update </EPPReference/CommandStructure/Update/UpdateDomain>`,
* :doc:`domain:renew </EPPReference/CommandStructure/RenewDomain>`,
* :doc:`contact:create </EPPReference/CommandStructure/Create/CreateContact>`,
* :doc:`contact:update </EPPReference/CommandStructure/Update/UpdateContact>`.

.. code-block:: xml
   :caption: Example of a command with an extension

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <create>
            <domain:create xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</domain:name>
               <domain:period unit="y">1</domain:period>
               <domain:registrant>CID-MYOWN</domain:registrant>
            </domain:create>
         </create>
         <!-- Extension of the standard command -->
         <extension>
            <enumval:create xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.0.xsd">
               <enumval:valExDate>2018-01-14</enumval:valExDate>
            </enumval:create>
         </extension>
         <clTRID>tucj013#17-07-14at16:22:30</clTRID>
      </command>
   </epp>

.. _response-ext:

Response extensions
~~~~~~~~~~~~~~~~~~~

Response extensions are extensions in the XPath :samp:`/epp/response/extension/*:*`.

According to the general requirements of the standard, the ``<extension>``
element is optional but if used then it must contain a sequence of one or more
elements (any namespace). The FRED EPP server requires the ``<extension>``
element to have a single child at most.

These extensions are used in response to the following commands:

* :doc:`domain:info </EPPReference/CommandStructure/Info/InfoDomain>`,
* :doc:`contact:info </EPPReference/CommandStructure/Info/InfoContact>`.

.. code-block:: xml
   :caption: Example of a response with an extension

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1000">
            <msg>Command completed successfully</msg>
         </result>
         <resData>
            <domain:infData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>1.2.2.4.5.0.2.4.e164.arpa</domain:name>
               <domain:roid>D0009770598-CZ</domain:roid>
               <domain:status s="outzone">The domain isn't generated in the zone</domain:status>
               <domain:registrant>C0-79371</domain:registrant>
               <domain:clID>REG-MYREG</domain:clID>
               <domain:crID>REG-MYREG</domain:crID>
               <domain:crDate>2017-05-18T17:04:29+02:00</domain:crDate>
               <domain:exDate>2018-05-18</domain:exDate>
               <domain:authInfo>LmpdDXW2</domain:authInfo>
            </domain:infData>
         </resData>
         <!-- Extension of the standard response -->
         <extension>
            <enumval:infData xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.0.xsd">
               <enumval:valExDate>2017-10-08</enumval:valExDate>
               <enumval:publish>0</enumval:publish>
            </enumval:infData>
         </extension>
         <trID>
            <clTRID>klde004#17-05-30at15:28:16</clTRID>
            <svTRID>ReqID-0000135159</svTRID>
         </trID>
      </response>
   </epp>
