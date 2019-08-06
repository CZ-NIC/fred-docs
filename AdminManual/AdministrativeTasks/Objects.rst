
.. _FRED-Admin-AdminTasks-Objects:

Objects administration
----------------------

All information about objects (registrable and other) can be browsed and viewed
via the WebAdmin after login.

To modify :term:`registrable object`\ s, you have to use an :doc:`EPP client
</Concepts/EPPClientWorkflow>` (e.g. :program:`fred-client`).

.. contents:: Chapter TOC
   :local:
   :backlinks: none

.. _modify-operations:

Operations to modify registrable objects
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The operations for registrable object modification encompass:

* check – see if an object can be registered,
* create – register a new object,
* delete – unregister an object,
* info – view object's details,
* renew – prolong a domain registration,
* sendauthinfo – request a transfer password,
* transfer – perform a transfer,
* update – change object's details.

These operations are typically performed by registrars
and they can be achieved only through the :ref:`Registrar interface
<interfaces-rif>`.
If you need to do any of these as the Registry, it is what
the **system registrar** is for.

Refer to the :doc:`/Concepts/EPPClientWorkflow` concept for details.

.. _view-objects-details:

View object's details
^^^^^^^^^^^^^^^^^^^^^

:ref:`Search <FRED-Admin-AdminTasks-Search>` for an object in the WebAdmin
and then click on its *id* or *handle* or *fqdn* to display the details.

If the search result contains only one record, you are redirected to its details.

.. Domains

.. _task-admin-blocking:

Administrative blocking of domains
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Blocking a domain means to withdraw it from the typical workflow
by forcing or prohibiting some operations over this domain.

State flags for blocking
~~~~~~~~~~~~~~~~~~~~~~~~

The blocking is achieved by setting various blocking state flags (prohibitions,
see also :doc:`/Concepts/LifeCycle/index`).
Which flags are suitable, depends on each case and the purpose of blocking.

Sometimes you may need to block even the domain holder together with the domain
name, in which case the same blocking state flags are applied to both the owner
contact and the domain.

* *The domain is administratively kept out of zone* – forces the exclusion
  of a domain from the zone (overrides all rules for domain inclusion),
* *The domain is administratively kept in zone* – forces the inclusion
  of a domain in the zone (overrides all rules for domain exclusion),
* *Deletion forbidden* – prohibits the deletion of the domain/contact,
* *Registration renewal forbidden* – prohibits the prolongation of a domain
  registration,
* *Sponsoring registrar change forbidden* – prohibits the transfer
  of the domain/contact,
* *Update forbidden* – prohibits changes of domain/contact details,
* *Registrant change forbidden* – prohibits to reassign the domain owner.

Block a domain
~~~~~~~~~~~~~~

To set a blocking of a single domain, follow this procedure:

#. In the WebAdmin, :ref:`view domain's details <view-objects-details>` and
   click the :guilabel:`Block` button at the bottom.
#. The form with blocking options appears. Fill in:

   * *Reason* – the reason why the domain(s) has(have) to be withdrawn
     from the usual flow (e.g. indication of a violated law or rule),
   * *Holder blocking* – decide what to do with the domain's owner:
      * ``Do not block the holder`` will not do anything with the registrant,
        they will be able to change any contact information or
        the designated registrar or to be deleted,
      * ``Block the holder`` will apply the same blocking flags
        to the registrant as the blocked domain(s) (this option can be selected
        only if you're blocking all domains of this registrant at once),
      * ``Create copy of the holder`` will duplicate the contact and apply
        the same blocking flags to the duplicate as to the domain being blocked
        while the other domains and the original contact remain intact.
   * *Block to date* – on this date, the blocking will be cancelled automatically,
   * *Blocking statuses* – select which blocking flags to turn on.

#. Apply the blocking by clicking the :guilabel:`Block` button
   and confirm with :guilabel:`OK`.

.. Note:: A blocked holder will be restored during domain unblocking automatically
   under certain conditions. See `Unblock a domain`_.

Change blocking of a domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~

If a domain already has been set some blocking flags, you can modify them
following this procedure:

#. In the WebAdmin, :ref:`view domain's details <view-objects-details>` and
   click the :guilabel:`Change blocking` button at the bottom.
#. The form with blocking options appears. Fill in:

   * *Reason* – the reason why the blocking is being changed,
   * *Block to date* – change the end of blocking or leave empty to keep
     the old value,
   * *Blocking statuses* – check or uncheck flags to change the blocking.

#. Apply the blocking by clicking the :guilabel:`Block` button
   and confirm with :guilabel:`OK`.

Unblock a domain
~~~~~~~~~~~~~~~~

To remove blocking flags from a domain, follow this procedure:

#. In the WebAdmin, :ref:`view domain's details <view-objects-details>` and
   click the :guilabel:`Unblock` button at the bottom.
#. The form with unblocking options appears. Fill in:

   * *Reason* – the reason why the domain is being unblocked,
   * *New holder* – assign a new owner by their *handle*,
   * *Remove admin. contacts* – unassign all administrative contacts,
   * *Restore prev. state* – restore the object state that was before blocking.

#. Proceed with the unblocking by clicking the :guilabel:`Unblock` button
   and confirm with :guilabel:`OK`.

The system removes all blocking flags, eventually restores the former set of
flags which used to be assigned before the blocking, if requested.

The system attempts to unblock the original owner contact, if it had been blocked
together with the domain, and if it is not linked to any other blocked domains.
If it is linked to other blocked domains, the system creates a copy of the owner
contact, replaces the original contact with the copy in the blocked domains,
and unblocks the original owner.

Blacklist and delete a domain
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A domain can be added to the Registry's blacklist,
so that it may not be re-registered for some time or at all.

#. In the WebAdmin, :ref:`view domain's details <view-objects-details>` and
   click the :guilabel:`Blacklist and delete` button at the bottom.
#. The form with blacklist options appears. Fill in:

   * *Reason* – the reason why the domain has to be blacklisted and deleted
     (e.g. indication of a violated law or rule),
   * *To* (date) – on this date, the domain will be made available
     for registrations again. Leave it empty to blacklist the domain indefinitely.

#. Confirm by clicking the :guilabel:`Blacklist and delete` button and then
   :guilabel:`OK`.

Blocking, unblocking, or blacklisting in bulk
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To block, unblock, change blocking of or blacklist a set of domains, follow
this procedure:

#. :ref:`Search <FRED-Admin-AdminTasks-Search>` domains to get those
   you need to block or blacklist.
#. Click the :guilabel:`Administrative blocking` link under the result table.
   It will allow you to select domains for blocking by using checkboxes.
   Check the box in the table header to select all displayed domains.
#. Above the result table, select which blocking operation you need to perform
   (block, change blocking, unblock, blacklist) and click :guilabel:`Start...`.
#. The blocking form appears that lets you set the blocking parameters
   for all selected domains at once. Options are the same as for the
   single-domain variant of these operations (see `block a domain`_,
   `change blocking of a domain`_, `unblock a domain`_ or `blacklist and
   delete a domain`_).
#. Proceed by clicking the button and confirm by :guilabel:`OK`.


.. Force include in the zone
   ~~~~~~~~~~~~~~~~~~~~~~~~~

   Daphne > domain details > :guilabel:`Set InZone Status`

   Force exclude from the zone
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
   Search emails mentioning this domain
   dig
   Inspect user actions in the audit log

.. Contacts

Contact verification :sup:`CZ-specific`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
:abbr:`TBD (to be developed)`

Enqueue contact for verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
View results of automatic verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Resolve manual verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _contact-merge:

Merge contacts
^^^^^^^^^^^^^^

The contact merger allows to fuse together two or more contacts that appear
to represent the same identity and that are in a merge-able state.

The contact merger can be used from the command line only.

The definition of merge-able contacts and the description of the merge
operation can be found in the :doc:`/Concepts/ContactMerger` concept.

.. _contact-merge-manual:

Merge a pair of duplicate contacts (manual)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Registry operator can use a manual merge and select a pair of duplicate
contacts by themself. The operator must also decide which contact will be
the *destination contact*, which will remain.

A pair of merge-able contacts can be then merged by running a command like this:

.. code-block:: shell

   fred-admin --contact_merge --src <src-contact-handle> --dst <dst-contact-handle> [--dry_run]

This command will :ref:`merge <merge-operation>` the *source contact* given
by its handle into the *destination contact* given by its handle.

The ``--dry_run`` option is available to preview what the command will do.
Also see the program ``--help`` for more options.

.. _contact-merge-auto:

Merge a set of duplicate contacts (automatic)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The automatic merge procedure should be set up as a :ref:`periodic task
<cronjob-contact-merger>`.

.. _resolve-public-request:

Resolve a public request
^^^^^^^^^^^^^^^^^^^^^^^^

The public has the option to request a transfer password, personal information,
or turn on/off enhanced security of their objects in the Registry database.

The form for request input and more details about the public requests can be
found on the default location: http://localhost/whois/publicrequest.py

The types of public requests:

* Sending password for transfer (authinfo)
* Blocking of transfer
* Unblocking of transfer
* Blocking of all changes
* Unblocking of all changes
* Sending personal information

Procedure to resolve a public request:

#. In the WebAdmin, select :menuselection:`Logs --> PublicRequests`.
#. :ref:`Search <FRED-Admin-AdminTasks-Search>` for unresolved requests
   (use the field *Status* with the value ``PRS_OPENED``).
#. View request's details.
#. If the request has been authorized, click the :guilabel:`Accept and send` button
   to answer it, otherwise click :guilabel:`Invalidate and close`.
   In both cases, you will be prompted for an extra confirmation by retyping
   a number. Type it and hit :guilabel:`OK`.
#. The request has been resolved.

.. _generate-rs:

Generate a record statement
^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. `View object's details`_ and scroll down.
#. Under the :guilabel:`Generate record statement` heading, select the date and
   time to which the record shall be retrieved from the history of registrations.
#. Click the :guilabel:`Download PDF` button.
#. The generated PDF file will start downloading shortly.
