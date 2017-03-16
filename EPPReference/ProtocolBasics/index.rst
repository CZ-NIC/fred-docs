


Protocol basics
===============

...

Message structure
-----------------

Command message
^^^^^^^^^^^^^^^

Contains the command with arguments.

Response message
^^^^^^^^^^^^^^^^

Contains the response to the called command with a
:doc:`return code and message </EPPReference/Appendices/ReturnCodes>`,
and sometimes even return values (``resData``).

.. _plain-result:

Plain result message
~~~~~~~~~~~~~~~~~~~~

def. "plain result" message = response that does not contain any resData

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
         <trID>
            <clTRID>sdmj001#17-03-06at18:48:03</clTRID>
            <svTRID>ReqID-0000126633</svTRID>
         </trID>
      </response>
   </epp>

Implemented commands
--------------------

* transfer, op="request"
