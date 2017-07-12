
.. index:: logout, Ⓔlogout

Logout
======

A logout command is used to end a session with the EPP server
established by a :doc:`Login` command.

The logout command is a ``logout`` element in the ``epp`` namespace
(``urn:ietf:params:xml:ns:epp-1.0``).

Command element structure
-------------------------

The ``<logout>`` element does not contain any child elements.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
       <command>
           <logout/>
           <clTRID>scui002#17-05-03at16:54:42</clTRID>
       </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > logout

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
       <response>
           <result code="1500">
               <msg>Command completed successfully; ending session</msg>
           </result>
           <trID>
               <clTRID>scui002#17-05-03at16:54:42</clTRID>
               <svTRID>ReqID-0000132660</svTRID>
           </trID>
       </response>
   </epp>
