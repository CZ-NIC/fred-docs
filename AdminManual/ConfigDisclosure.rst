Contact information disclosure
------------------------------

Disclosure of contact details must be configured in both the back end (fred-rifd)
and the front end (Apache module mod-eppd).

.. rubric:: mod-eppd

``EPPdataCollectionPolicyAccess`` -- sets the general approach and implies
the logic for contact preference requests (``create``/``update``) and display
(``info``):

* ``all`` -- the general approach is "Registry shows information",
  registrars shall use ``flag='0'`` to signal contact preference
  to hide listed attributes,
* ``none`` -- the general approach is "Registry hides information",
  registrars shall use ``flag='1'`` to signal contact preference
  to show listed attributes.

:samp:`EPPcontact{Operation}Discloseflags` lists names of the elements that
can be used in the disclose element of the corresponding operation.

.. Important:: The ``*Discloseflags`` lists must allow the same elements
   that are allowed in the XSD schemas!

.. rubric:: fred-rifd

``contact_data_filter`` -- a method of enforcing server's disclosure policy:

* ``set_unused_discloseflags`` -- sets disclosure of attributes, for which
  there was no preference, to the configured defaults unconditionally
* ``cznic_specific`` -- controls conditional disclosure of *address*
  (see :ref:`epp-rules-hiding-address`),
  sets other disclosure settings, for which there was no preference,
  to the configured defaults unconditionally

The Registry operator may develop and assign custom methods.

Default disclosure settings ``default_disclose*`` are listed for ``create`` and
``update`` operations separately. If the attribute's disclosure cannot be set
in an operation, it must have a default setting listed here.

Example configurations
^^^^^^^^^^^^^^^^^^^^^^

.. rubric:: Pre-GDPR configuration with the :term:`CZ-specific` filter
   (as in version 2.36)

.. code-block:: apacheconf
   :caption: mod-eppd

   EPPdataCollectionPolicyAccess all
   EPPcontactCreateDiscloseflags telephone fax email vat ident notifyemail
   EPPcontactUpdateDiscloseflags address telephone fax email vat ident notifyemail
   EPPcontactInfoDiscloseflags address telephone fax email vat ident notifyemail

.. code-block:: ini
   :caption: fred-rifd

   [rifd]
   contact_data_filter = cznic_specific
   [rifd::cznic_specific::create_contact]
   default_disclosename = show
   default_discloseorganization = show
   default_discloseaddress = show
   [rifd::cznic_specific::update_contact]
   default_disclosename = show
   default_discloseorganization = show


.. rubric:: GDPR-compliant configuration with the :term:`CZ-specific` filter
   (as in version 2.37)

.. code-block:: apacheconf
   :caption: mod-eppd

   EPPdataCollectionPolicyAccess none
   EPPcontactCreateDiscloseflags telephone fax email vat ident notifyemail
   EPPcontactUpdateDiscloseflags address telephone fax email vat ident notifyemail
   EPPcontactInfoDiscloseflags address telephone fax email vat ident notifyemail

.. code-block:: ini
   :caption: fred-rifd

   [rifd]
   contact_data_filter = cznic_specific
   [rifd::cznic_specific::create_contact]
   default_disclosename = show
   default_discloseorganization = show
   default_discloseaddress = show
   [rifd::cznic_specific::update_contact]
   default_disclosename = show
   default_discloseorganization = show


.. rubric:: GDPR-compliant configuration without the :term:`CZ-specific` filter

.. code-block:: apacheconf
   :caption: mod-eppd

   EPPdataCollectionPolicyAccess none
   EPPcontactCreateDiscloseflags telephone fax email vat ident notifyemail
   EPPcontactUpdateDiscloseflags address telephone fax email vat ident notifyemail
   EPPcontactInfoDiscloseflags address telephone fax email vat ident notifyemail

.. code-block:: ini
   :caption: fred-rifd

   [rifd]
   contact_data_filter = set_unused_discloseflags
   [rifd::set_unused_discloseflags::create_contact]
   default_disclosename = show
   default_discloseorganization = show
   default_discloseaddress = show
   [rifd::set_unused_discloseflags::update_contact]
   default_disclosename = show
   default_discloseorganization = show
