


Introduction
============

...

Conventions for the description of XML structures
-------------------------------------------------

*Element names* are represented enclosed between the lower-than
and the greater-than sign in a similar way as in actual XML documents,
e.g. ``<nameSpace:elementName>``.

After the element name, the number of allowed
*occurrences* of the element is stated within parentheses and in bold,
e.g. **(1..3)** means between one and three occurrences of an element,
**(0..1)** means an optional element,
**(1)** means an element must occur exactly once,
**(1..n)** means that an element must occur at least once
but the maximum number of occurrences is unbound, and so on.

*Children of an element* are formatted as a sub-list, hence indentation models
the tree structure of XML.

*Attribute names* are prefixed with an ``@``, e.g. ``@attributeName``.
After the attribute name, the *use of the attribute* is specified
if it is different from the default (attributes are optional), that is
**(R)** if the attribute is required or **(P)** if the attribute is prohibited.

Element and attribute names are also generated to the *index*
under the Symbols section. They are prefixed either with an Ⓔ for elements
or with an ⓐ for attributes, so that they are distinguished
from general index keys.
