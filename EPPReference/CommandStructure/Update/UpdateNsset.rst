
.. index:: update; nsset

Update nsset
=============


A nsset update :ref:`command <struct-command>` is used to alter details of a nsset.

The nsset update command is an ``update`` element in the ``nsset`` namespace
(``http://www.nic.cz/xml/epp/nsset-1.2``).

The command must be contained in the ``<update>`` command type.

.. index:: Ⓔupdate, Ⓔid, Ⓔadd, Ⓔrem, Ⓔchg, Ⓔns, Ⓔname, Ⓔaddr, Ⓔtech,
   ⒺauthInfo, Ⓔreportlevel

Command element structure
-------------------------

The ``<nsset:update>`` element must declare the ``nsset`` namespace
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<nsset:id>`` **(1)**  – a nsset handle as :term:`fredcom:objIDType`,
* ``<nsset:add>`` **(0..1)** – a list of items that will be added to this nsset:

   * ``<nsset:ns>`` **(0..10)** – a nameserver given by:
      * ``<nsset:name>`` **(1)** – a nameserver hostname as :term:`eppcom:labelType`,
      * ``<nsset:addr>`` **(0..n)** – a namesever's IP address as :term:`nsset:addrStringType`,
   * ``<nsset:tech>`` **(0..n)** –  a handle of a contact that will be added
     as a technical contact as :term:`fredcom:objIDType`,

* ``<nsset:rem>`` **(0..1)** – a list of items that will be removed
  from this nsset:

   * ``<nsset:name>`` **(0..n)** – a nameserver hostname as :term:`eppcom:labelType`,
   * ``<nsset:tech>`` **(0..n)** – a handle of nsset's technical contact as :term:`fredcom:objIDType`,

* ``<nsset:chg>`` **(0..1)** – the new values of nsset attributes
  that will be replaced by this update. Omitted attributes will remain unchanged.

   * ``<nsset:authInfo>`` **(0..1)** – change the nsset's authorization
     information (transfer password) as :term:`fredcom:authInfoType`,
   * ``<nsset:reportlevel>`` **(0..1)** – change the level of technical checks
     to be reported as :term:`nsset:reportlevelType`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
   <command>
      <update>
         <nsset:update xmlns:nsset="http://www.nic.cz/xml/epp/nsset-1.2"
          xsi:schemaLocation="http://www.nic.cz/xml/epp/nsset-1.2 nsset-1.2.xsd">
            <nsset:id>NID-MYNSSET</nsset:id>
            <nsset:add>
               <nsset:ns>
                  <nsset:name>ns.otherdomain.cz</nsset:name>
                  <nsset:addr>217.31.207.130</nsset:addr>
                  <nsset:addr>217.31.207.131</nsset:addr>
               </nsset:ns>
               <nsset:tech>CID-TECH2</nsset:tech>
            </nsset:add>
            <nsset:rem>
               <nsset:name>ns2.mydomain.cz</nsset:name>
               <nsset:tech>CID-TECH1</nsset:tech>
            </nsset:rem>
            <nsset:chg>
               <nsset:reportlevel>4</nsset:reportlevel>
            </nsset:chg>
         </nsset:update>
      </update>
      <clTRID>kgev002#17-07-18at15:38:08</clTRID>
   </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > update_nsset NID-MYNSSET (((ns.otherdomain.cz (217.31.207.130, 217.31.207.131))) CID-TECH2) (ns2.mydomain.cz CID-TECH1) NULL 4

Response element structure
--------------------------

The FRED EPP server responds with a :ref:`plain result message <plain-result>`
which does not contain any response data (no ``<resData>``).

See also :ref:`succ-fail`.
