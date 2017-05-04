
.. index::
   pair: delete; contact

Delete contact
==============

A contact delete command is a ``delete`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

It is used to delete a contact whose status allows it to be deleted.

.. index:: Ⓔdelete, Ⓔid

Command element structure
-------------------------

The ``<contact:delete>`` element must declare the ``contact`` namespace
and schema and it must contain the following child element:

* ``<contact:id>`` **(1)** the contact handle as :term:`fredcom:objIDType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
      <delete>
         <contact:delete
          xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.xsd">
            <contact:id>CID-MYCONTACT</contact:id>
         </contact:delete>
      </delete>
      <clTRID>fyem005#17-05-04at22:22:12</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > delete_contact CID-MYCONTACT

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result <plain-result>` message
which does not contain any return values (no ``resData``).
