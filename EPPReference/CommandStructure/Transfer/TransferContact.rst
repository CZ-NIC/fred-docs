
.. index::
   pair: transfer; contact

Transfer contact
================

A contact transfer :ref:`command <struct-command>` is used to take over
sponsorship of a contact.
The transfer password of the contact must be provided for authorization.

A new password is generated for the contact by the server after a successful transfer.

The contact transfer command is a ``transfer`` element in the ``contact`` namespace
(``http://www.nic.cz/xml/epp/contact-1.6``).

The command must be contained in the ``<transfer>`` command type.
The command type must specify the request operation (``@op = 'request'``).

.. index:: Ⓔtransfer, Ⓔid, ⒺauthInfo

Command element structure
-------------------------

The ``<contact:transfer>`` element must declare the ``contact`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<contact:id>`` **(1)** – the contact handle as :term:`fredcom:objIDType`,
* ``<contact:authInfo>`` **(1)**  – the transfer password as :term:`fredcom:authInfoType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <transfer op="request">
            <contact:transfer xmlns:contact="http://www.nic.cz/xml/epp/contact-1.6"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/contact-1.6 contact-1.6.2.xsd">
               <contact:id>CID-TRCONT</contact:id>
               <contact:authInfo>trpwd</contact:authInfo>
            </contact:transfer>
         </transfer>
         <clTRID>gcnd002#17-08-01at13:00:14</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > transfer_contact CID-TRCONT trpwd

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
