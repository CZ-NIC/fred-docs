
.. index::
   pair: delete; domain

Delete domain
==============

A domain delete :ref:`command <struct-command>` is used to delete a domain
whose status allows it to be deleted.

The domain delete command is a ``delete`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

The command must be contained in the ``<delete>`` command class.

.. index:: Ⓔdelete, Ⓔname

Command element structure
-------------------------

The ``<domain:delete>`` element must declare the ``domain`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child element:

* ``<domain:name>`` **(1)** – the domain name as :term:`eppcom:labelType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
      <delete>
         <domain:delete xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
            <domain:name>mydomain.cz</domain:name>
         </domain:delete>
      </delete>
      <clTRID>zuhv011#17-05-05at14:51:57</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > delete_domain mydomain.cz

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
