
.. _FRED-Admin-AdminTasks-Registrars:

Registrar administration
------------------------

All registrar information can be managed via the WebAdmin after login.

List all registrars
^^^^^^^^^^^^^^^^^^^

Select in the WebAdmin menu: :menuselection:`Registrars --> List`

Or run on the command line ``sudo fred-admin --registrar_list`` (XML output
containing all registrars' details).

View registrar's details
^^^^^^^^^^^^^^^^^^^^^^^^

`List all registrars`_ or :ref:`search <FRED-Admin-AdminTasks-Search>`
for a registrar in the WebAdmin and then click on its *handle* to display
the details.

Add a registrar
^^^^^^^^^^^^^^^
To add a new registrar in the WebAdmin, follow this procedure:

#. Select :menuselection:`Registrars --> Create new` from the menu
   to display the edit form and fill it in:

   * Registrar data – contact and billing information
     (*handle* and *country* are mandatory)
   * Authentication – password and MD5 sum of the certificate for EPP connection
   * Zones – grant access to zones
   * Groups – assign membership in groups
     (you may need to `create a group`_ first)
   * Certifications – evaluation of registrar's retail services
     (it can be used in the public overview of registrars (default location:
     http://localhost/whois/registrars.py,
     see also the `Certification programme in the CZ.NIC
     <https://www.nic.cz/page/928/>`_)

#. Click the :guilabel:`Save` button to save the new registrar.

Or provide the details on the command line. (See the program help
for command parameters.)

* Registrar data: ``sudo fred-admin --registrar_add <parameters>``
* Authentication: ``sudo fred-admin --registrar_acl_add <parameters>``
* Zones: ``sudo fred-admin --registrar_add_zone <parameters>``
* Groups: ``sudo fred-admin --registrar_into_group <parameters>``
* Certifications: ``sudo fred-admin --registrar_create_certification <parameters>``

.. _daphne-task-registrar-edit:

Edit registrar's details
^^^^^^^^^^^^^^^^^^^^^^^^
To modify registrar's information, use the WebAdmin:

#. `View registrar's details`_, then scroll to the bottom and click
   :guilabel:`Edit` to display the edit form.
#. Edit the details (see `Add a registrar`_ for a description of the details).
#. Click the :guilabel:`Save` button, when you finish, to save the changes.

Registrar blocking
^^^^^^^^^^^^^^^^^^
Blocking a registrar means that their EPP access is suspended
until the end of the current month. The usual reason is that a registrar
wants to cease activity when their monthly budget for EPP requests is exhausted.

Block a registrar
~~~~~~~~~~~~~~~~~

Registrars are blocked by the system automatically
if they exceed their preset price limit for EPP requests and
the :ref:`periodic task to block registrars over limit <block-registrars-limit>`
is set up.

Registrars cannot be blocked via the WebAdmin.

In case of emergency, a registrar can be blocked on the command line::

   sudo fred-admin --block_registrar_id <registrar_id>

.. Note:: If a registrar was unblocked this month,
   they cannot be blocked again till the next month.

Unblock a registrar
~~~~~~~~~~~~~~~~~~~

A registrar can be unblocked via the WebAdmin:

#. `View registrar's details`_, scroll down and click the :guilabel:`Unblock`
   button.
#. You will be prompted for an extra confirmation by retyping a number.
   Type it and hit :guilabel:`OK`.
#. The registrar is unblocked.

Or on the command line::

   sudo fred-admin --unblock_registrar_id <registrar_id>

Registrar groups
^^^^^^^^^^^^^^^^
Registrar groups are handy when you want to categorize the registrars,
e.g. to mark which of them support DNSSEC or IPv6.

To view the list of groups, select in the WebAdmin menu:
:menuselection:`Registrars --> Groups`

You can **change membership in a group** when you `edit registrar's details`_.

Create a group
~~~~~~~~~~~~~~

In the list of groups, find the last (empty) form field, enter the name
of a new group and click :guilabel:`Save`.

Or provide the details on the command line:
``sudo fred-admin --registrar_create_group <parameters>``
(see the program help for parameters).

Rename a group
~~~~~~~~~~~~~~

In the list of groups, find the group you want to rename, rewrite the name
in the form field and click :guilabel:`Save`.

Remove a group
~~~~~~~~~~~~~~

In the list of groups, find the group you want to delete, check
the :guilabel:`Delete` checkbox and click :guilabel:`Save`.

.. Note:: The WebAdmin lets you remove only empty groups.

.. _daphne-task-assign-payment:

Assign a payment to a registrar
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If a payment was imported to the database but it could not be matched
with a registrar automatically, you can do so manually in the WebAdmin:

#. To view the list of payments, select in the WebAdmin menu:
   :menuselection:`Registrars --> Payments`

#. Search for the *Not assigned* payments or restrict the search further,
   should there be too many results, and choose a payment to view its details.

#. Select the *From/to registrar* type of payment.

#. Enter the *Registrar's handle* to pair the payment with.

#. Confirm the input by clicking :guilabel:`Save`.
   You will be prompted for an extra confirmation by retyping a number.
   Type it and hit :guilabel:`OK`.

#. The pairing is saved. (If the payment was sufficient, registrar's credit
   has been increased.)

.. NOTE The type of payment must correspond with an appropriate destination
   account if you have various accounts for various purposes. Where is this set?
