
.. index::
   pair: delete; nsset

Delete nsset
==============

A nsset delete :ref:`command <struct-command>` is used to delete a nsset
whose status allows it to be deleted.

The nsset delete command is a ``delete`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

The command must be contained in the ``<delete>`` command type.

.. index:: Ⓔdelete, Ⓔid

Command element structure
-------------------------

The ``<nsset:delete>`` element must declare the ``nsset`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
      <delete>
         <nsset:delete xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.2.xsd">
            <nsset:id>NID-MYNSSET</nsset:id>
         </nsset:delete>
      </delete>
      <clTRID>ripo005#17-05-05at15:21:44</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > delete_nsset NID-MYNSSET

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
