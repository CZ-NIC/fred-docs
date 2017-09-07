
.. _mng-domain:

Domains
-------

A domain contains information which represents a regular domain or
an :term:`ENUM` domain.

Namespace: \http://www.nic.cz/xml/epp/domain-1.4 |br|
Schema: domain-1.4.2.xsd

.. Note:: Domain name mapping is based on the standard :rfc:`5731`
   but it is not entirely compliant.

.. _mng-domain-attr:

Object attributes
^^^^^^^^^^^^^^^^^

In addition to the :ref:`common attributes <common-attrs>`, domains also have
the following attributes:

``name``
   The domain name. See :ref:`mngobj-domain-syntax`.

``registrant``
   The :ref:`handle <mngobj-handle-syntax>` of the domain owner contact.

``admin``
   The :ref:`handle <mngobj-handle-syntax>`\ (s) of zero or more administrative contact(s).

``nsset``
   The :ref:`handle <mngobj-handle-syntax>` of a nameserver set.

``keyset``
   The :ref:`handle <mngobj-handle-syntax>` of a DNSSEC-key set.

``exDate``
   The date of domain name expiration.

``valExDate`` :sup:`ENUM only`
   The date of the expiration of ENUM domain validation.

``publish`` :sup:`ENUM only` :sup:`+ DEPRECATED`
   Flag of publishing an ENUM domain in a public ENUM directory.

   This attribute has currently no meaning for the server and it will be removed
   in the future. Use of this attribute is discouraged.

.. _mng-domain-stat:

Object states
^^^^^^^^^^^^^^^^^

A domain can have one or more of the following statuses:

* ``ok`` – no other states are set
* ``serverDeleteProhibited`` – deletion of the domain is forbidden
* ``serverRenewProhibited`` – renewal of the domain is forbidden
* ``serverTransferProhibited`` – transfer of the domain is forbidden
* ``serverUpdateProhibited`` – update of the domain is forbidden
* ``serverRegistrantChangeProhibited`` – the change of the registrant of the domain is forbidden
* ``serverBlocked`` – the domain is blocked by administration
* ``serverOutzoneManual`` – domain's absence in the zone is forced by administration
* ``serverInzoneManual`` – domain's presence in the zone is forced by administration
* ``expired`` – the domain is expired
* ``outzone`` – the domain is not included in the zone
* ``notValidated`` :sup:`ENUM only` – the ENUM domain is not validated
* ``deleteCandidate`` – the domain is scheduled for deletion

.. _mng-domain-map:

Command-response mapping
^^^^^^^^^^^^^^^^^^^^^^^^

For command-response mapping see a specific command syntax description:

* :doc:`domain:check </EPPReference/CommandStructure/Check/CheckDomain>`
* :doc:`domain:create </EPPReference/CommandStructure/Create/CreateDomain>`
* :doc:`domain:delete </EPPReference/CommandStructure/Delete/DeleteDomain>`
* :doc:`domain:info </EPPReference/CommandStructure/Info/InfoDomain>`
* :doc:`domain:renew </EPPReference/CommandStructure/RenewDomain>`
* :doc:`domain:transfer </EPPReference/CommandStructure/Transfer/TransferDomain>`
* :doc:`domain:update </EPPReference/CommandStructure/Update/UpdateDomain>`
* :doc:`domain:sendAuthInfo </EPPReference/CommandStructure/SendAuthInfo/SendAuthInfoDomain>`

.. top-level elements

   command TLE: ``<domain:check>``, ``<domain:create>``, ``<domain:delete>``,
   ``<domain:info>``, ``<domain:renew>``, ``<domain:transfer>``, ``<domain:update>``,
   ``<domain:sendAuthInfo>`` :sup:`EXT`

   response data TLE: ``<domain:chkData>``, ``<domain:creData>``, ``<domain:infData>``,
   ``<domain:renData>``

   poll msg TLE: ``<domain:trnData>``, ``<domain:impendingExpData>``, ``<domain:expData>``,
   ``<domain:dnsOutageData>``, ``<domain:delData>``, ``<domain:updateData>``

   ENUM poll msg TLE: ``enumval:impendingValExpData``, ``enumval:valExpData``

ENUM domains
^^^^^^^^^^^^

ENUM domains have the same set of attributes as regular domains except for two
additional attributes. Therefore they are managed by the same commands &
responses as regular domains, only the handling of the additional attributes
requires the extensions of the standard commands & responses,
so that these attributes can be included in transactions where appropriate.

Namespace: \http://www.nic.cz/xml/epp/enumval-1.2 |br|
Schema: enumval-1.2.0.xsd

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
* :doc:`domain:renew </EPPReference/CommandStructure/RenewDomain>`.

.. code-block:: xml
   :caption: Example of a command with an extension

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <create>
            <domain:create xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
               <domain:name>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</domain:name>
               <domain:period unit="y">1</domain:period>
               <domain:registrant>CID-MYOWN</domain:registrant>
            </domain:create>
         </create>
         <!-- Extension of the standard command -->
         <extension>
            <enumval:create xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.xsd">
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

These extensions are used only in response to the
:doc:`domain:info </EPPReference/CommandStructure/Info/InfoDomain>` command.

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
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.1.xsd">
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
