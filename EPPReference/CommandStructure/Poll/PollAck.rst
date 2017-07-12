


Poll acknowledge
================

Command element structure
-------------------------

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <poll msgID="18856172" op="ack"/>
         <clTRID>kkel002#17-03-08at16:12:47</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > poll ack 18856172

Response element structure
--------------------------

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1000">
            <msg lang="cs">Příkaz úspěšně proveden</msg>
         </result>
         <msgQ count="1" id="18862843"/>
         <trID>
            <clTRID>kkel002#17-03-08at16:12:47</clTRID>
            <svTRID>ReqID-0000126713</svTRID>
         </trID>
      </response>
   </epp>
