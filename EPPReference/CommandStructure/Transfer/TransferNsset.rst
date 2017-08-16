
.. index::
   pair: transfer; nsset

Transfer nsset
================

A nsset transfer command is used to take over the management of a nsset.
A transfer password must be provided for authorization.
It can be the transfer password of:

* the nsset, or
* a technical contact of the nsset.

A nsset transfer command is a ``transfer`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

.. index:: Ⓔtransfer, Ⓔid, ⒺauthInfo

Command element structure
-------------------------

The command class must specify the request operation (``@op = 'request'``).

The ``<nsset:transfer>`` element must declare the ``nsset`` namespace
and schema and it must contain the following child elements:

* ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:authInfo>`` **(1)**  – the transfer password as :term:`fredcom:authInfoType`.

.. rubric:: Example

.. code-block:: xml

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <transfer op="request">
            <nsset:transfer xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.xsd">
               <nsset:id>NID-TRNSSET</nsset:id>
               <nsset:authInfo>trpwd</nsset:authInfo>
            </nsset:transfer>
         </transfer>
         <clTRID>yoie002#17-08-01at13:15:51</clTRID>
      </command>
   </epp>

.. rubric:: FRED-client equivalent

.. code-block:: shell

   > transfer_nsset NID-TRNSSET trpwd

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
