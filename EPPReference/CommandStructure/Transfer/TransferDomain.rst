
.. index::
   pair: transfer; domain

Transfer domain
===============

A domain transfer :ref:`command <struct-command>` is used to take over
sponsorship of a domain.
A transfer password must be provided for authorization.
It can be the transfer password of:

* the domain,
* the domain owner contact, or
* an administrative contact of the domain.

A new password is generated for the domain by the server after a successful transfer.

The domain transfer command is a ``transfer`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

The command must be contained in the ``<transfer>`` command class.
The command class must specify the request operation (``@op = 'request'``).

.. index:: Ⓔtransfer, Ⓔname, ⒺauthInfo

Command element structure
-------------------------

The ``<domain:transfer>`` element must declare the ``domain`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<domain:name>`` **(1)**  – a domain name as :term:`eppcom:labelType`,
* ``<domain:authInfo>`` **(1)**  – the transfer password as :term:`fredcom:authInfoType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
      <transfer op="request">
         <domain:transfer xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.xsd">
            <domain:name>trdomain.cz</domain:name>
            <domain:authInfo>trpwd</domain:authInfo>
         </domain:transfer>
      </transfer>
      <clTRID>zhbf002#17-07-25at16:34:40</clTRID>
   </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > transfer_domain trdomain.cz trpwd

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
