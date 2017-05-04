
.. index::
   pair: delete; nsset

Delete nsset
==============

A nsset delete command is a ``delete`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

It is used to delete a nsset whose status allows it to be deleted.

.. index:: Ⓔdelete, Ⓔid

Command element structure
-------------------------

The ``<nsset:delete>`` element must declare the ``nsset`` namespace
and schema and it must contain the following child element:

* ``<nsset:id>`` **(1)** the nsset handle as :term:`fredcom:objIDType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
      <delete>
         <nsset:delete xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.xsd">
            <nsset:id>NID-MYNSSET</nsset:id>
         </nsset:delete>
      </delete>
      <clTRID>ripo005#17-05-05at15:21:44</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > delete_nsset NID-MYNSSET

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result <plain-result>` message
which does not contain any return values (no ``resData``).
