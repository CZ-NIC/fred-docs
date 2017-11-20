
.. _FRED-EPPRef-Intro:

Introduction
============

This is a reference manual for the EPP protocol as implemented by the FRED.

The global XSD schema ``all-2.4.0`` has been taken as the **baseline** for the reference.

The manual describes protocol basics and the generic structure of messages
in a nutshell (based on the main RFC standard), introduces registrable objects
managed in the FRED, contains basic guidelines on the use of the namespaces
and schemas and finally embraces an overview and a detailed reference
of specific commands and responses, all interleaved with examples.
Appendices contain overviews of result codes, error reasons and simple data
types from schemas.



Conventions for describing XML structures
-------------------------------------------------

To describe XML structures, the following notation is used.

**Element names** are represented enclosed between the lower-than
and the greater-than sign in a similar way as in actual XML documents,
e.g. ``<nameSpace:elementName>``. If a namespace prefix is collapsed
into an asterisk, e.g. ``<*:elementName>``, it means that the element is used
(similarly) in several namespaces and these should be listed somewhere nearby.

After the element name, the number of allowed
**occurrences** of the element is stated within parentheses and in bold,
e.g. **(1..3)** means between one and three occurrences of an element,
**(0..1)** means an optional element,
**(1)** means an element must occur exactly once,
**(1..n)** means that an element must occur at least once
but the maximum number of occurrences is unbound, and so on.

**Children of an element** are formatted as a sub-list, hence indentation models
the tree structure of XML. Although the lists are not numbered, elements must
appear in the order they are listed. If a sub-list is introduced with the phrase
**one of**, then the sub-list represents possible choices (only one of the
listed elements may appear) instead of a sequence.

**Attribute names** are prefixed with an ``@``, e.g. ``@attributeName``.
After the attribute name, the **use of the attribute** is specified
if it is different from the default (attributes are optional), that is
**(R)** if the attribute is required or **(P)** if the attribute is prohibited.

Element and attribute names are also generated to the **index**
`under the Symbols section <../../genindex.html#Symbols>`_.
They are prefixed either with an Ⓔ for elements
or with an ⓐ for attributes, so that they are distinguished
from general index keys.
