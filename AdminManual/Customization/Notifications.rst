


Customizing state-change notifications
---------------------------------------

State-change notifications are the part of Registry email communication
that is based on the life cycle of :term:`registrable object`\ s,
in other words, on *state changes* of registrable objects.

See also :ref:`comm-objlife` for the table of lifecycle-based notifications.

**These notifications can be disabled** by removal of rows from the database
table ``notify_statechange_map``:

.. code-block:: sql

   fred=> select * from notify_statechange_map;
    id | state_id | obj_type | mail_type_id | emails
   ----+----------+----------+--------------+--------
     1 |        9 |        3 |            3 |      1
     2 |       20 |        3 |            4 |      1
     3 |       17 |        3 |            5 |      1
     4 |       17 |        2 |           14 |      1
     5 |       17 |        1 |           14 |      1
     6 |       20 |        3 |            6 |      2
     7 |       17 |        3 |            7 |      2
     8 |       12 |        3 |            8 |      1
     9 |       13 |        3 |            9 |      1
    10 |       13 |        3 |            6 |      2
    11 |       17 |        4 |           14 |      1
    12 |       28 |        3 |           31 |      3
    13 |       28 |        3 |           31 |      4
   (13 rows)

This table says: when an object of the type ``obj_type`` is set the status flag
``state_id``, an email message of the type ``mail_type_id`` is sent to recipients
according to ``emails``.

.. rubric:: Object states

See the table ``enum_object_states`` and compare with :doc:`/Concepts/LifeCycle/index`.

.. rubric:: Object types

``obj_type`` is the type of an object to be notified (1..contact, 2..nsset,
3..domain, 4..keyset), see the table ``enum_object_type``.

.. rubric:: Mail types

``mail_type_id`` is the type of mail to be sent from the table ``mail_type``,
see also :doc:`/AdminManual/Appendixes/EmailParameters`.

.. _custom-notif-recipients:

.. rubric:: Email recipients

``emails`` are only distinguished in case of domains:

* 1 -- all administrative contacts of the domain
* 2 -- all technical contacts of the domain's nsset
* 3 -- *generic* emails, see :ref:`communication channels <comm-channels>`
* 4 -- *additional* domain notification emails, see :ref:`communication channels <comm-channels>`

In case of nssets or keysets, recipients are all technical contacts.

In case of contacts, recipient is the contact itself.
