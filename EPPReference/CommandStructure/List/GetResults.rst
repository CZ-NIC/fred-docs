
.. index:: getResults

Get the results
===============

This command is used to retrieve the list of objects that was prepared
in the previous step with a list command.

This command is a :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

The command is a ``getResults`` element in the ``fred`` namespace
(``http://www.nic.cz/xml/epp/fred-1.5``).

Command element structure
-------------------------

The ``<fred:getResults/>`` element does not contain any child elements.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <extension>
      <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
       xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.xsd">
         <fred:getResults/>
         <fred:clTRID>ovcu003#17-08-11at12:27:01</fred:clTRID>
      </fred:extcommand>
   </extension>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > get_results

Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the standard result, response data and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<fred:resultsList>`` which declares the ``fred`` namespace and schema
and it contains the following child elements:

* ``<fred:item>`` **(0..n)** – an item of the results list as :term:`xs:token`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <response>
      <result code="1000">
         <msg>Command completed successfully</msg>
      </result>
      <resData>
         <fred:resultsList xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.0.xsd">
            <fred:item>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</fred:item>
            <fred:item>mydomain.cz</fred:item>
            <fred:item>thisdomain.cz</fred:item>
            <fred:item>trdomain.cz</fred:item>
         </fred:resultsList>
      </resData>
      <trID>
         <clTRID>ovcu003#17-08-11at12:27:01</clTRID>
         <svTRID>ReqID-0000141135</svTRID>
      </trID>
   </response>
   </epp>
