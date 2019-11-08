
Localization
============

Basic languages for Ferda are English and Czech.

If you want to add another language, you have to add locales both in Python
and JavaScript.

Localizing Python
-----------------

Python uses the *gettext* system where locales are stored in message
files (.po).

Generate a message file for the new language using the command
`django-admin makemessages -l <language>` command from the root of the
Ferda app.

Translate the strings into the target language.

You need to compile them with the command `django-admin compilemessages`
before deployment.

Localizing JavaScript
---------------------

JavaScript stores translations in the `yaml
<https://learnxinyminutes.com/docs/yaml/>` format.

Ferda has locales in the directory :file:`ferda/static/ferda/locales/`,
which contains a subdirectory for each language.

Copy the contents of one of them (e.g. from :file:`en`) to a new directory
named after the target language (e.g. :file:`es`).

Translate the strings into the target language.

Setting up the new language
----------------------------

After creating localizations, you need to enable them for use in Ferda.

To set up your new language (e.g. Spanish) in the settings file,
modify the following variables:

.. code-block:: python
   :caption: Localization setting example

   LANGUAGE_CODE = 'es' # the default language
   LANGUAGES = (
       ('en', 'English'),
       ('cs', 'Česky'),
       ('es', 'Español'),
   )

If a translation string is missing, the localization falls back to the English
string.
