
.. index::
   pair: transfer; keyset

Transfer keyset
================

A keyset transfer command is used to take over the management of a keyset.
A transfer password must be provided for authorization.
It can be the transfer password of:

* the keyset, or
* a technical contact of the keyset.

A keyset transfer command is a ``transfer`` element in the ``keyset`` namespace
(``http://www.nic.cz/xml/epp/keyset-1.3``).

.. index:: Ⓔtransfer, Ⓔid, ⒺauthInfo

Command element structure
-------------------------

The command class must specify the request operation (``@op = 'request'``).

The ``<keyset:transfer>`` element must declare the ``keyset`` namespace
and schema and it must contain the following child elements:

* ``<keyset:id>`` **(1)** – the keyset handle as :term:`fredcom:objIDType`,
* ``<keyset:authInfo>`` **(1)**  – the transfer password as :term:`fredcom:authInfoType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <transfer op="request">
            <keyset:transfer xmlns:keyset="http://www.nic.cz/xml/epp/keyset-1.3"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/keyset-1.3 keyset-1.3.xsd">
               <keyset:id>KID-TRKEYSET</keyset:id>
               <keyset:authInfo>trpwd</keyset:authInfo>
            </keyset:transfer>
         </transfer>
         <clTRID>skmb002#17-08-01at13:22:08</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > transfer_keyset KID-TRKEYSET trpwd

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
