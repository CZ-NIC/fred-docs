
.. _epp-disc-examples:

Examples of behaviour
---------------------

.. contents:: Examples overview
   :local:
   :backlinks: none

.. _epp-disc-examples-create:

``contact:create`` command
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Request – without the element ``<contact:disclose>``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The EPP request does not contain ``<contact:disclose>``

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - hide

Requests to show listed attributes – ``<contact:disclose flag="1">``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Request – empty element ``<contact:disclose>``
''''''''''''''''''''''''''''''''''''''''''''''

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - hide

Request – show all you can
''''''''''''''''''''''''''

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:voice/>
     <contact:fax/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:voice/>
     <contact:fax/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - show
     - show
     - show
     - show
     - show
     - show

Request – show a specified subset
'''''''''''''''''''''''''''''''''

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - show
     - show
     - show
     - hide

Requests to hide listed attributes – ``<contact:disclose flag="0">``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These requests don't make sense when the policy is to *hide*; it always
results in a contact having all disclosure settings set to *hide* except
for *address* which can't be set in the operation ``create`` and is set
to *show*.

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - hide

.. _epp-disc-examples-update:

``contact:update`` command
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Request – without the element ``<contact:disclose>``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Contact disclosure settings before the request:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - show

The EPP request does not contain ``<contact:disclose>``

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:notifyEmail/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - show

Requests to show listed attributes – ``<contact:disclose flag="1">``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The result depends on the contact, whether it satisfies conditions for
hiding *address* and the element ``<addr/>`` is listed in the request.

.. list-table::
   :header-rows: 1

   * - Element :code:`<addr/>` listed in the request
     - Contact satisfies conditions for hiding address
     - Result
   * - NO
     - NO
     - :code:`code=2304 msg=Object status prohibits operation`
   * - NO
     - YES
     - :code:`code=1000 msg=Command completed successfully`
   * - YES
     - NO
     - :code:`code=1000 msg=Command completed successfully`
   * - YES
     - YES
     - :code:`code=1000 msg=Command completed successfully`

Request – empty element ``<contact:disclose>`` – contact does NOT satisfy conditions for hiding address
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
   </contact:disclose>

The request results in an error:

.. code-block:: xml

   <result code="2304">
      <msg>Object status prohibits operation</msg>
   </result>

Request – empty element ``<contact:disclose>`` – contact DOES satisfy conditions for hiding address
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Contact disclosure settings before the request:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1"/>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - hide
     - hide

Request – show all you can
''''''''''''''''''''''''''

Contact disclosure settings before the request:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:voice/>
     <contact:fax/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:voice/>
     <contact:fax/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - show
     - show
     - show
     - show
     - show
     - show

Request – show a specified subset – contact does NOT satisfy conditions for hiding address (and ``<addr/>`` is NOT listed)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

The request results in an error:

.. code-block:: xml

   <result code="2304">
      <msg>Object status prohibits operation</msg>
   </result>

Request – show a specified subset – contact does NOT satisfy conditions for hiding address (and ``<addr/>`` IS listed)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Contact disclosure settings before the request:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - show
     - hide
     - hide
     - show
     - show

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:addr/>
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - hide
     - show
     - show
     - show
     - show

Request – show a specified subset – contact DOES satisfy conditions for hiding address
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Contact disclosure settings before the request:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - show
     - hide
     - show
     - hide
     - hide
     - show
     - show

The EPP request contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Result – the response to ``contact:info`` contains:

.. code-block:: xml

   <contact:disclose flag="1">
     <contact:email/>
     <contact:vat/>
     <contact:ident/>
     <contact:notifyEmail/>
   </contact:disclose>

Interpretation of the result:

.. list-table::
   :header-rows: 1

   * - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - ident
     - notifyemail
   * - show
     - show
     - hide
     - hide
     - hide
     - show
     - show
     - show
     - show

Requests to hide listed attributes – ``<contact:disclose flag="0">``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These requests don't make sense when the policy is to *hide*; it results
in:

* **an error** if the contact does not satisfy conditions for hiding
  *address*:

  .. code-block:: xml

     <result code="2304">
       <msg>Object status prohibits operation</msg>
     </result>

* otherwise, all disclosure settings being set to *hide*:

  .. list-table::
     :header-rows: 1

     * - name
       - organization
       - address
       - telephone
       - fax
       - email
       - vat
       - ident
       - notifyemail
     * - show
       - show
       - hide
       - hide
       - hide
       - hide
       - hide
       - hide
       - hide
