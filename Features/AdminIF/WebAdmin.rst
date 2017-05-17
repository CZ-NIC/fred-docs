
.. _FRED-Features-Admin-Web:

Web admin features
-------------------

Webadmin features are divided into feature groups which also constitute
the sections of this document.


General
^^^^^^^

* User authentication on login
* User must be permitted to perform an action (The granularity of permissions
  corresponds with the atomic operations over objects: read, change, block,
  unblock, delete, add.)
* Show/hide the history of details (set globally per session)
* Extra confirmation for critical actions (e.g. domain blocking)
* Referenced objects are linked by hypertext (object handles, attached files)

Configurables
~~~~~~~~~~~~~

* User authentication method
* User authorization method and permissions
* Table page size (number of rows per page)
* Table timeout
* Table maximum row limit (general and object-specific)
* Calendar date format for viewing and editing
* Utility for calculating termination dates of domain blocking and blacklisting
* Lock duration to resolve a verification check
* Limit of the wait for a response to a manual verification check request



Result table properties
^^^^^^^^^^^^^^^^^^^^^^^

* Result tables paginated
   * With page navigation
      * Go to the first / previous / next / last page
      * Go to a page by number
* Even and odd table rows distinguished (different background color)
* Table row highlighted when hovered over
* Sort table by any column (ascending or descending)
* If the result contains only a single record, view its details directly
* Export results to TXT or CSV



Compose a search filter
^^^^^^^^^^^^^^^^^^^^^^^

* Add a field (logical AND)
* Remove a field
* Add an alternative statement (logical OR)
* Remove an alternative statement
* Negate a field (logical NOT)
* Un-negate a field
* Save the current filter using a custom name
* Use a saved filter
* Show a saved filter



Manage domains
^^^^^^^^^^^^^^

* Search/filter domains
* Select domains
* Administer blocking of multiple (selected) domains
   * Block
   * Change blocking
   * Unblock
   * Blacklist and delete
* View domain details
   * List emails from the last month where this domain is mentioned
   * View dig details about this domain
   * Include domain in the zone manually
   * View related logs (List logged actions in the last month by various Service types)
   * Block this domain
   * Change blocking of this domain
   * Unblock this domain
   * Blacklist and delete this domain



Browse contacts
^^^^^^^^^^^^^^^
* Search/filter contacts
* View contact details
   * List domains where this contact is an owner
   * List domains where this contact is an admin
   * List all domains where this contact appears in any role (owner/admin/temp)
   * List all NSSets where this contact is a technical contact
   * List all KeySets where this contact is a technical contact
   * List emails from the last month where this contact is mentioned
   * List public requests concerning this contact
   * List all messages for this contact
   * List all verification checks of this contact
   * Enqueue contact for automatic verification
   * Enqueue contact for manual verification
   * View related logs (List logged actions in the last month by various Service types)



Verify contacts
^^^^^^^^^^^^^^^

* List contact checks by type (automatic/manual/all)
* View contact check details – Automatic
* Resolve check
   * Resolve as failed
   * Invalidate
   * Resolve as OK
* View contact check details – Manual
* Resolve check
   * Confirm enqueue
   * Invalidate
   * Resolve as OK



Browse NS sets
^^^^^^^^^^^^^^

* Search/filter NSSets
* View NSSet details
   * List domains with this NSSet
   * List emails in the last month where this NSSet is mentioned
   * View related logs (List logged actions in the last month by various Service types)



Browse key sets
^^^^^^^^^^^^^^^

* Search/filter KeySets
* View KeySet details
   * List domains with this KeySet
   * List emails from the last month where this KeySet is mentioned
   * View related logs (List logged actions in the last month by various Service types)



Manage registrars
^^^^^^^^^^^^^^^^^

* List all registrars
* Search/filter registrars
* View registrar details
* Add a new registrar
* Edit registrar details
   * Registrar data (contact and billing info)
   * Authentication
   * Zones
   * Groups
   * Certifications
* Manage registrar groups
   * Add group
   * Rename group
   * Delete group (only empty)



Browse invoices
^^^^^^^^^^^^^^^

* Search/filter invoices
* View invoice details



Browse and assign payments
^^^^^^^^^^^^^^^^^^^^^^^^^^

* Search/filter payments
* View payment details
   * Assign a type to a not-assigned payment
      * Associate a not-assigned payment with a registrar



Browse audit log
^^^^^^^^^^^^^^^^

* Search/filter logs (from logger)
* View log details



Browse and resolve public requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

What is a :term:`public request`?

* Search/filter public requests
* View request details
* Resolve the request
   * Accept and send
   * Invalidate and close
   * Resend a copy of PIN3 Letter (used in contact verification)
   * Resend a copy of PIN2 SMS (used in contact verification)



Browse sent emails
^^^^^^^^^^^^^^^^^^

* Search/filter emails
* View email details



Browse sent messages
^^^^^^^^^^^^^^^^^^^^

* Search/filter messages (emails, letters, sms texts, registered letters)
* View message details



Browse files
^^^^^^^^^^^^

* Search/filter files
* (List domain expiration warning letters) (predefined filter)
* Download a file
