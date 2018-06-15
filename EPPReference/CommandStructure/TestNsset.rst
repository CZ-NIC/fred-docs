
.. index:: test, techcheck

Test nsset
===========

A nsset test command is used to request
a :doc:`technical check </Concepts/Teccheck>` of an nsset.

The check is not performed immediately but it is scheduled for execution.
After the tests have finished, a report is provided to the client
in :ref:`poll messages <epp-poll-type-techcheck>`.

The nsset test command is a ``test`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

The command must be contained in the ``<fred:test>`` command type.

This command is a part of the :doc:`protocol extension </EPPReference/ProtocolBasics/ProtocolExtensions>`
defined by the FRED EPP server.

.. index:: Ⓔextcommand, Ⓔtest, Ⓔid, Ⓔlevel, Ⓔname

Command element structure
-------------------------

The ``<nsset:test>`` element must declare the ``nsset`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<nsset:id>`` **(1)** – the nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:level>`` **(0..1)** – the highest level of tests to be performed
  as :term:`nsset:reportlevelType`,
* ``<nsset:name>`` **(0..n)** – additional domain names to be tested
  with the nsset as :term:`eppcom:labelType` (applies only to some tests).

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <extension>
         <fred:extcommand xmlns:fred="http://www.nic.cz/xml/epp/fred-1.5"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/fred-1.5 fred-1.5.0.xsd">
            <!-- Custom command type -->
            <fred:test>
               <!-- The object-defined command -->
               <nsset:test xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
                xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.2.xsd">
                  <nsset:id>NID-MYNSSET</nsset:id>
                  <nsset:level>5</nsset:level>
                  <nsset:name>mydomain.cz</nsset:name>
                  <nsset:name>somedomain.cz</nsset:name>
               </nsset:test>
            </fred:test>
            <fred:clTRID>loxj006#17-08-01at14:51:33</fred:clTRID>
         </fred:extcommand>
      </extension>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > technical_test NID-MYNSSET 5 (mydomain.cz,somedomain.cz)

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
