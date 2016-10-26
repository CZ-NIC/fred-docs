
.. _FRED-Admin-AdminTasks-Search:

Database search
---------------

.. Compose a search filter (from Featues)

   * Add a field (logical AND)
   * Remove a field
   * Add an alternative statement (logical OR)
   * Remove an alternative statement
   * Negate a field (logical NOT)
   * Un-negate a field
   * Save the current filter using a custom name
   * Use a saved filter
   * Show a saved filter

The WebAdmin allows you to search any objects in the database,
typically Registrars or registrable objects but also archived mail and messages,
public requests or the audit log.

This is the general search procedure:

#. First, you select from the WebAdmin menu what kind of objects you want
   to search (e.g. :menuselection:`Objects --> Search domains`).

#. You continue with composing a search filter in which you specify search
   criteria. It can be a simple query, such as a search for a domain by its
   handle, or a complex statement combining many attributes and logical
   operations (``and``, ``or``, ``not``).

#. Start the search by clicking the :guilabel:`OK` button.
   You can also save the search filter for a later use
   under a name of your choice by clicking the :guilabel:`Save` button.

   A saved search filter will appear above the search form as a text link.

#. If results are found, they are displayed in the *result table*
   below the search form. Results can be sorted by any column by clicking
   the column header.

   To view the details of a record, click the icon in the *id* column.
   If the search result contains only one record, the details are displayed
   directly.

.. Note:: The column collection of the result table is hard-coded
   and it can not be adjusted.

.. NOTE
   * saved filters - are there any default ones?
      no, only the "custom filter" link
   * search field selection ?
