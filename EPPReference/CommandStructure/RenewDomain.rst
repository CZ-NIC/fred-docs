
.. index::
   pair: renew; domain


Renew domain
============

A domain renew :ref:`command <struct-command>` is used to prolong
the registration of a domain name.

The domain renew command is a ``renew`` element in the ``domain`` namespace
(``http://www.nic.cz/xml/epp/domain-1.4``).

The command must be contained in the ``<renew>`` command type.

.. index:: Ⓔrenew, Ⓔname, ⒺcurExpDate, Ⓔperiod, ⓐunit

Command element structure
-------------------------

The ``<domain:renew>`` element must declare the ``domain`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>` and it must contain the following child elements:

* ``<domain:name>`` **(1)**  – the domain name as :term:`eppcom:labelType`,
* ``<domain:curExpDate>`` **(1)**  – the domain's current expiration date
  as :term:`xs:date`,
* ``<domain:period>`` **(0..1)**  – the prolongation period
  as :term:`domain:pLimitType`,

   * ``@unit`` **(R)**  – the unit in which the period is counted; it can be
     either ``m`` for months or ``y`` for years.

  .. Note:: The prolongation period must be a multiple of the allowed step
     and it must be in the allowed range for prolongation in the zone according
     to the registration rules of the Registry.

     The FRED's default minimum and the allowed step is 1 year. The FRED's default
     maximum is 10 years.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <renew>
            <domain:renew xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>mydomain.cz</domain:name>
               <domain:curExpDate>2018-07-11</domain:curExpDate>
               <domain:period unit="y">2</domain:period>
            </domain:renew>
         </renew>
         <clTRID>xykf008#17-07-13at19:14:56</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > renew_domain mydomain.cz 2018-07-11 (2 y)

.. index:: ⒺvalExDate, Ⓔpublish

ENUM extension
^^^^^^^^^^^^^^

The ``<domain:renew>`` element is used in the same way as described above.

The :ref:`command extension <command-ext>` can be used to prolong the validation
of an ENUM domain together with prolongation of expiration. If you need
to change the validation independently, use the
:doc:`domain:update <Update/UpdateDomain>` command.

The command's ``<extension>`` element must contain a **single** ``<enumval:renew>``
element which declares the ``enumval`` namespace (``http://www.nic.cz/xml/epp/enumval-1.2``)
and :doc:`schema </EPPReference/SchemasNamespaces/index>` and contains:

* ``<enumval:valExDate>`` **(0..1)**  – a new validation expiration date as :term:`xs:date`,

  .. _new-valexdate:

  .. Note::

     Before the actual validation expiration date, there is a period of time
     which allows to prolong the validation relatively to the old validation
     expiration date and thus seemingly exceed the allowed maximum for validation.
     This period is called the "continuation window"
     and its duration depends on the Registry policy.

     FRED's default continuation window is 14 days. FRED's default validation
     period is 6 months.

     The ``new valExDate`` must be in the range depending on the current date:

     * if ``today`` is in the continuation window, the ``new valExDate`` can range
       from ``tomorrow`` to ``old exValDate + validation period`` (inclusive),
     * otherwise the ``new valExDate`` can range from ``tomorrow``
       to ``today + validation period`` (inclusive).

* ``<enumval:publish>`` **(0..1)** – a new setting for publishing the ENUM
  domain in a public directory as :term:`xs:boolean`;
  ``true`` – display, ``false`` – hide.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="utf-8" standalone="no"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <command>
         <renew>
            <domain:renew xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa</domain:name>
               <domain:curExpDate>2018-07-14</domain:curExpDate>
               <domain:period unit="y">1</domain:period>
            </domain:renew>
         </renew>
         <extension>
            <enumval:renew xmlns:enumval="http://www.nic.cz/xml/epp/enumval-1.2"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/enumval-1.2 enumval-1.2.0.xsd">
               <enumval:valExDate>2018-01-14</enumval:valExDate>
            </enumval:renew>
         </extension>
         <clTRID>vzic002#17-07-14at18:55:41</clTRID>
      </command>
   </epp>

.. code-block:: shell
   :caption: FRED-client equivalent

   > renew_domain 1.1.1.7.4.5.2.2.2.0.2.4.e164.arpa 2018-07-14 (1 y) 2018-01-14


Response element structure
--------------------------

The :ref:`response <struct-response>` from the FRED EPP server contains
the result, response data, and transaction identification.

See also :ref:`succ-fail`.

The response data element (``<resData>``) contains a single child element
``<domain:renData>`` which declares the ``domain`` :doc:`namespace and schema </EPPReference/SchemasNamespaces/index>`
and it contains the following child elements:

* ``<domain:name>`` **(1)** – the domain name as :term:`eppcom:labelType`,
* ``<domain:exDate>`` **(0..1)** – the new expiration date of the domain name
  after renewal as :term:`xs:date`.

.. code-block:: xml
   :caption: Example

   <?xml version="1.0" encoding="UTF-8"?>
   <epp xmlns="urn:ietf:params:xml:ns:epp-1.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="urn:ietf:params:xml:ns:epp-1.0 epp-1.0.xsd">
      <response>
         <result code="1000">
            <msg>Command completed successfully</msg>
         </result>
         <resData>
            <domain:renData xmlns:domain="http://www.nic.cz/xml/epp/domain-1.4"
             xsi:schemaLocation="http://www.nic.cz/xml/epp/domain-1.4 domain-1.4.2.xsd">
               <domain:name>mydomain.cz</domain:name>
               <domain:exDate>2020-07-11</domain:exDate>
            </domain:renData>
         </resData>
         <trID>
            <clTRID>xykf008#17-07-13at19:14:56</clTRID>
            <svTRID>ReqID-0000139811</svTRID>
         </trID>
      </response>
   </epp>

ENUM extension
^^^^^^^^^^^^^^

:ref:`Response extension <response-ext>` is not used in reply to this command.
