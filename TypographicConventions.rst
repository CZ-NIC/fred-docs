:orphan:

.. _typocon:

Typographic Conventions
=======================

Font styles
-----------

*italics*

* general light in-line emphasis
* labels of elements in user interfaces (button names, form field labels,
  tab and window titles, menu selections)

**bold**

* general strong in-line emphasis
* names of executables (programs, scripts)

``monospace``

* file names, directory names, paths
* names of parameters, variables and arguments
* commands and code snippets
* names of modules, libraries and packages
* constant values and other literals

Links
-----

External and internal links are differentiated with the following styling:

* :ref:`internal link <typocon>`
* `external link <http://www.example.com>`_

Code snippets
-------------

Code snippets are set in a monospace font and they are highlighted
according to the language of the snippet. Example:

.. code-block:: bash

   #!/bin/bash
   variable="Hello world!"
   echo $variable

Special characters
------------------

.. rubric:: Angle brackets < >

Angle brackets are sometimes used in code illustrations, like this:

.. code-block:: bash

   # Running a program
   program-name <arguments>

The ``<arguments>`` part suggests that program arguments should follow.
The text inside the brackets gives a hint on the type of arguments, however
if you are uncertain, consult the program help.

Concrete arguments are usually entered *without* the brackets!

.. rubric:: Square brackets [ ]

Square brackets usually signify something optional, like command arguments
that may be used (or not used), unless specified otherwise. Again, if you decide
to use an optional argument, enter it *without* the brackets.

Admonitions
-----------

Admonitions are used to highlight a block of text that has special importance.
Several types of admonitions are distinguished by their severity/importance:

.. Warning:: advisory information that states that performing some action
   may lead to serious or dangerous consequences (what the user must not do)

.. Caution:: advisory information that states that performing some action
   may lead to consequences that are unwanted or undefined, such as loss of data
   or an equipment problem (what the user should not do)

.. Important:: advisory information that states that a certain action must
   be performed where inaction may lead to unwanted or undefined consequences
   (what the user must do)

.. Note:: advisory information in addition to the surrounding text
   (what the user should know)

.. Tip:: advisory information how to use a product more efficiently or in a way
   that is not apparent (what the user can do or know)

Authoring notes
---------------

Authoring notes—or TODOs—usually hold suggestions for new topics or notes
about pending improvements. The TODOs are visible in the text, if their output
is allowed in project configuration.

.. todo:: This is an authoring note. The TODOs are on.
   :class: todo-backlog

If you cannot see a green rectangle before this paragraph, the TODO output is disabled.

Semantic markup overview
------------------------

This overview exists just for checking that semantic markup has correct
styling.

In-line:

* :abbr:`ABBR (explanation)` – abbreviation with an explanation (:rst:role:`abbr`)
* :file:`file.txt` – file name (:rst:role:`file`)
* :guilabel:`Cancel` – GUI label (:rst:role:`guilabel`)
* :menuselection:`Menu --> Submenu --> Option` – menu selection (:rst:role:`menuselection`)
* :program:`script.sh` – program name (:rst:role:`program`)
* :term:`FQDN` – link to a term definition in the glossary (:rst:role:`term`)
* :code:`in-line code` or ``in-line code`` – in-line code (:rst:role:`code` role or ````literal````)
