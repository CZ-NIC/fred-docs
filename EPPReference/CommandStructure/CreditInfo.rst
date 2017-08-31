
.. index::
   pair: credit; info

Credit info
===========

A credit info command is used to find out about
the current credit amounts of the authenticated registrar in all zones
for which the registrar is accredited.

The credit info command is a ``creditInfo`` element in the ``fred`` namespace
(``http://www.nic.cz/xml/epp/fred-1.5``).

This command is a part of the :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

.. index:: ⒺcreditInfo

Command element structure
-------------------------

The ``<fred:creditInfo/>`` element does not contain any child elements.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <extension>
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">
         <fred:creditInfo/>
         <fred:clTRID>hlxk002#17-05-18at16:55:06</fred:clTRID>
      </fred:extcommand>
      </extension>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > credit_info

.. index:: ⒺresCreditInfo, ⒺzoneCredit, Ⓔzone, Ⓔcredit

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<fred:resCreditInfo>`` which declares the ``fred`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<fred:zoneCredit>`` **(0..n)** – the credit information of a single zone:
   * ``<fred:zone>`` **(1)** – the zone FQDN as :term:`eppcom:labelType`,
   * ``<fred:credit>`` **(1)** – the amount of credit in this zone as :term:`fred:amountType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
      <result code="1000">
         <msg>Command completed successfully</msg>
      </result>
      <resData>
         <fred:resCreditInfo xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.0.xsd">
            <fred:zoneCredit>
               <fred:zone>0.2.4.e164.arpa</fred:zone>
               <fred:credit>66112.00</fred:credit>
            </fred:zoneCredit>
            <fred:zoneCredit>
               <fred:zone>cz</fred:zone>
               <fred:credit>82640.00</fred:credit>
            </fred:zoneCredit>
         </fred:resCreditInfo>
      </resData>
      <trID>
         <clTRID>hlxk002#17-05-18at16:55:06</clTRID>
         <svTRID>ReqID-0000133058</svTRID>
      </trID>
      </response>
   </epp>
