
.. index::
   pair: delete; keyset

Delete keyset
==============

A keyset delete command is a ``delete`` element in the ``keyset`` namespace
(``http://www.nic.cz/xml/epp/keyset-1.3``).

It is used to delete a keyset whose status allows it to be deleted.

.. index:: Ⓔdelete, Ⓔid

Command element structure
-------------------------

The ``<keyset:delete>`` element must declare the ``keyset`` namespace
and schema and it must contain the following child element:

* ``<keyset:id>`` **(1)** the keyset handle as :term:`fredcom:objIDType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
      <delete>
         <keyset:delete xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.xsd">
            <keyset:id>KID-MYKEYSET</keyset:id>
         </keyset:delete>
      </delete>
      <clTRID>osnc004#17-05-05at15:44:51</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > delete_keyset KID-MYKEYSET

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result <plain-result>` message
which does not contain any return values (no ``resData``).