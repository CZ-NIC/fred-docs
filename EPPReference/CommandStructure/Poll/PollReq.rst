


Poll request
=============

Command element structure
-------------------------

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <poll op="req"/>
         <clTRID>uqtv002#17-03-08at16:01:03</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > poll req

Response element structure
--------------------------

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1301">
            <msg lang="cs">Příkaz úspěšně proveden; potvrď za účelem vyřazení z fronty</msg>
         </result>
         <msgQ count="2" id="18856172">
            <qDate>2017-03-07T02:24:09+01:00</qDate>
            <msg>
               <fred:requestFeeInfoData xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5">
                  <fred:periodFrom>2017-03-01T00:00:00+01:00</fred:periodFrom>
                  <fred:periodTo>2017-03-06T23:59:59+01:00</fred:periodTo>
                  <fred:totalFreeCount>25000</fred:totalFreeCount>
                  <fred:usedCount>49</fred:usedCount>
                  <fred:price>0.00</fred:price>
               </fred:requestFeeInfoData>
            </msg>
         </msgQ>
         <trID>
            <clTRID>uqtv002#17-03-08at16:01:03</clTRID>
            <svTRID>ReqID-0000126711</svTRID>
         </trID>
      </response>
   </epp>
