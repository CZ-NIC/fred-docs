
.. index::
   pair: delete; contact

Delete contact
==============

A contact delete :ref:`command <struct-command>` is used to delete a contact
whose status allows it to be deleted.

The contact delete command is a ``delete`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

The command must be contained in the ``<delete>`` command type.

.. index:: Ⓔdelete, Ⓔid

Command element structure
-------------------------

The ``<contact:delete>`` element must declare the ``contact`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<contact:id>`` **(1)** – the contact handle as :term:`fredcom:objIDType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
      <delete>
         <contact:delete
          xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
            <contact:id>CID-MYCONTACT</contact:id>
         </contact:delete>
      </delete>
      <clTRID>fyem005#17-05-04at22:22:12</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > delete_contact CID-MYCONTACT

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
