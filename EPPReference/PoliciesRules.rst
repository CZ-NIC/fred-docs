


Policies & rules of disclosure
================================

There are some built-in policies and rules concerning contact information disclosure
to third-party entities, which include the public.

The contact information that is subject to the data collection policy and disclosure
policy entails these :doc:`contact attributes <ManagedObjects/Contacts>`:
*name*, *organization*, *address* (:code:`<addr/>`), *telephone* (:code:`<voice/>`),
*fax* (:code:`<fax/>`), *email* (:code:`<email/>`), *vat* (:code:`<vat/>`),
*identity document* (:code:`<ident/>`), *notify email* (:code:`<notifyEmail/>`).

Clients (registrars) are not considered third-party entities in the FRED,
and they deal with the information under terms of a contract with the Registry
operator.

The policies comply with :term:`GDPR` and they are currently hard-coded.

.. contents:: Chapter TOC
   :local:
   :backlinks: none
   :depth: 2


Data collection policy
----------------------

This policy is expressed in the :doc:`greeting <ProtocolBasics/ServiceDiscovery>`
from the EPP server, in the element :code:`<dcp>` (data collection policy);
*hide* is expressed as :code:`<access><none/></access>` and can be checked e.g.
by examining that the xpath :code:`/epp/greeting/dcp/access/none` is an
existing node.

This says that the policy of the server is to disclose none of the data
collected over EPP to third-party entities. However, this policy has exceptions
arising from the disclosure policy of the server and individual disclosure
preferences of each contact.


Server disclosure policy
------------------------

The server disclosure policy defines the default disclosure preference (flag)
for each attribute and also says which attribute's disclosure preference is adjustable
by contacts.

The server's default disclosure preference is to **hide all** personal information **except**
*name* and *organization*, which are always visible, and *address*, which
is forced visible on creation, but is hidden later when certain conditions are met
(see `Hiding address`_). Visibility of other contact attributes can be adjusted
on demand as explained in `Contact disclosure preference`_.

.. list-table:: Summary – Server disclosure policy
   :header-rows: 1
   :stub-columns: 1

   * - Attributes
     - name
     - organization
     - address
     - telephone
     - fax
     - email
     - vat
     - identity
     - notifyemail
   * - Default flags (contact:create)
     - show
     - show
     - show
     - hide
     - hide
     - hide
     - hide
     - hide
     - hide
   * - Nature
     - fixed
     - fixed
     - adjustable *
     - adjustable
     - adjustable
     - adjustable
     - adjustable
     - adjustable
     - adjustable

Server disclosure preference also means, that responses to ``contact:info``
use ``flag="1"`` to describe contact disclosure preference, i.e. which attributes
are *shown* as opposed to the server's default disclosure preference.


Contact disclosure preference
-----------------------------

The contact disclosure preference expresses an opposite of the server disclosure preference
where it is allowed by the policy to be adjusted. With the server disclosure preference to hide data,
the contact disclosure preference represents consent to disclose a piece of personal information.

To set or view disclosure preference, the :code:`<contact:disclose>` element is used.
Its syntax is described in the reference of each command:

* viewing disclosure preference with :ref:`contact:info <contact-infdata>`;

* setting disclosure preference with :doc:`contact:create <CommandStructure/Create/CreateContact>`
  is allowed for the attributes: |br|
  *telephone* (:code:`<voice/>`),
  *fax* (:code:`<fax/>`), *email* (:code:`<email/>`), *vat* (:code:`<vat/>`),
  *identity document* (:code:`<ident/>`), *notify email* (:code:`<notifyEmail/>`);

* setting disclosure preference with :doc:`contact:update <CommandStructure/Update/UpdateContact>`
  is allowed for the attributes: |br|
  *address* (:code:`<addr/>`), *telephone* (:code:`<voice/>`),
  *fax* (:code:`<fax/>`), *email* (:code:`<email/>`), *vat* (:code:`<vat/>`),
  *identity document* (:code:`<ident/>`), *notify email* (:code:`<notifyEmail/>`).

Disclosure preference for *name* and *organization* cannot be adjusted,
therefore they are never listed in requests nor responses.

If the contact does not satisfy the conditions for `hiding address`_, then
:code:`<addr/>` must be listed in update requests that are based on ``flag="1"``.

See also the :ref:`examples <epp-disc-examples>` at the end of this chapter.

Hiding address
--------------

When a new contact is being created, the contact disclosure preference for *address*
cannot be requested and the server uses its default disclosure preference,
which is to **show** *address*.

Once the contact [#cont-natur]_ is verified (has the status flag ``identifiedContact``)
or validated (has the status flag ``validatedContact``), the server changes
the disclosure preference for *address* to "**hide**" automatically and
notifies the client (the designated registrar) about this change in a poll message.
At this point, the contact is allowed to change it.

When the contact [#cont-natur]_ loses both verification and validation, the server changes
the disclosure preference for *address* back to "**show**" automatically and
notifies the client (the designated registrar) about this change in a poll message.
At this point, the contact cannot change it.

When the contact [#cont-natur]_ regains verification or validation, the same thing happens
as if it has gained it for the first time, see above. The contact disclosure
preference for *address* is ignored and overwritten.

.. [#cont-natur] This works only for contacts of natural persons, i.e. contacts
   that have the attribute *organization* without a value.

.. Note::

   The :code:`<addr/>` disclose flag affects disclosure of **all addresses**
   in a contact.

.. include:: Disclosure_Examples.rst
