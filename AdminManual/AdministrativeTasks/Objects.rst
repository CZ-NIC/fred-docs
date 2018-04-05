
.. _FRED-Admin-AdminTasks-Objects:

Registrable objects administration
----------------------------------

All information about objects can be browsed and viewed via the WebAdmin
after login.

To modify objects, you have to use an EPP client (e.g. :program:`fred-client`).

Operations to modify objects
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The operations for object modification encompass:

* check – see if an object can be registered,
* create – register a new object,
* delete – unregister an object,
* info – view object's details,
* renew – prolong a domain registration,
* sendauthinfo – request a transfer password,
* transfer – perform a transfer,
* update – change object's details.

These operations are typically performed by registrars
and they can be achieved only through the EPP interface.
If you need to do any of these as the Registry, it is what
the **system registrar** is for.

Refer to the help of the :program:`fred-client` program for the descriptions
of command usage.

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

Blocking statuses
~~~~~~~~~~~~~~~~~
The blocking is achieved by setting various blocking statuses.
Which statuses are suitable depends on the case and the purpose of blocking.
Sometimes you may need to block even the owner together with the domain
in which case the same blocking statuses are applied to both the owner contact
and the domain.

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
      * ``Block the holder`` will apply the same blocking statuses
        to the registrant as the blocked domain(s) (this option can be chosen
        only if you're blocking all domains of this registrant at once),
      * ``Create copy of the holder`` will duplicate the contact and apply
        the same blocking statuses to the duplicate as to the domain being blocked
        while the other domains and the original contact remain intact.
   * *Block to date* – on this date, the blocking will be cancelled automatically,
   * *Blocking statuses* – select which blocking statuses to turn on.

#. Apply the blocking by clicking the :guilabel:`Block` button
   and confirm with :guilabel:`OK`.

.. Note:: A blocked contact cannot be restored, you will have to use another one
   when unblocking the domain.

Change blocking
~~~~~~~~~~~~~~~
If a domain already has been set some blocking statuses, you can modify them
following this procedure:

#. In the WebAdmin, :ref:`view domain's details <view-objects-details>` and
   click the :guilabel:`Change blocking` button at the bottom.
#. The form with blocking options appears. Fill in:

   * *Reason* – the reason why the blocking is being changed,
   * *Block to date* – change the end of blocking or leave empty to keep
     the old value,
   * *Blocking statuses* – check or uncheck statuses to change the blocking.

#. Apply the blocking by clicking the :guilabel:`Block` button
   and confirm with :guilabel:`OK`.

Unblock a domain
~~~~~~~~~~~~~~~~
To remove blocking statuses from a domain, follow this procedure:

#. In the WebAdmin, :ref:`view domain's details <view-objects-details>` and
   click the :guilabel:`Unblock` button at the bottom.
#. The form with unblocking options appears. Fill in:

   * *Reason* – the reason why the domain is being unblocked,
   * *New holder* – assign a new owner by their *handle*,
   * *Remove admin. contacts* – unassign all administrative contacts,
   * *Restore prev. state* – restore the state (owner) that was before blocking.

#. Proceed with the unblocking by clicking the :guilabel:`Unblock` button
   and confirm with :guilabel:`OK`.

The system removes all blocking statuses.
It does not unblock the original owner in any case.

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

Blocking or blacklisting in bulk
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
   `change blocking`_, `unblock a domain`_ or `blacklist and delete a domain`_).
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
   (use the field *Status* with the value ``PRS_NEW``).
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
