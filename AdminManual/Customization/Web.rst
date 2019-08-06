
Customizing public web interface
---------------------------------

The *public web interface* (see also :ref:`interfaces-pif`)
is sourced as the component :program:`fred-webwhois`.
It is a standard **Django application**.

.. Note:: We give quickstart tips in this customization tutorial, however,
   we recommend you to familiarize yourself with the `Django framework
   <https://docs.djangoproject.com/en/1.11/intro/>`_.

   Also notice that there is a difference between
   `a Django app and a Django project
   <https://stackoverflow.com/questions/19350785/what-s-the-difference-between-a-project-and-an-app-in-django-world>`_.

The :file:`fred-webwhois` app has some *templates* and *views*.
It does not have any *models*, since it handles data through CORBA calls.

The public web interface can be divided into 3 feature groups:

* whois lookup -- a form for web WHOIS search, results and details about registered objects,
* registrar listing -- a list of accredited registrars and their details,
* public requests -- forms and responses for submission of requests from the public.

These feature groups are not stricly separated in the code, they are only used
in this documentation for better clarity.

.. todo::
   :class: todo-backlog

   * structure of template blocks (inheritance, nesting)
   * webwhois extension of template tags

Redesigning stylesheets
^^^^^^^^^^^^^^^^^^^^^^^

If you need to adapt the visual style only, changing CSS should suffice.

Create a folder for stylesheets under the :file:`static/webwhois` directory
of the :program:`fred-webwhois` app, such as ``css``,
and put your stylesheet(s) in there.

Then you have to add a reference to your stylesheet file(s) in the template
that contains the HTML head (by default in the :ref:`base template
<custom-web-template-base>`) as follows:

.. code-block:: django
   :caption: Link to a stylesheet in a template

   <link rel="stylesheet" type="text/css" href="{% static "webwhois/css/mystyle.css" %}"/>

You should use the ``static`` tag and a path relative to the static directory.
Django will render this expression to the full file path accordingly.

Before deployment, you must collect static files (e.g. images, JavaScript, CSS)
to a single location, see `Django 1.11: Managing static files
<https://docs.djangoproject.com/en/1.11/howto/static-files/>`_.

Reconfiguring URLs
^^^^^^^^^^^^^^^^^^

The URL patterns of the public web interface are composed as
:samp:`http(s)://{hostname}/{base-path}/{app-paths}`.

The scheme, *hostname*, and eventually the *base path* are defined
in web-server configuration.

The webwhois *app-paths* suffixes look like this by default
(strings following the *base path*):

* (empty suffix) -- the whois lookup form,
* ``registrars/`` -- the list of registrars,
* ``send-password/`` -- the public request to send authinfo password,
* and so on (the list is not complete).

You can find the *app-paths* configuration in ``webwhois/urls.py``
of the :program:`fred-webwhois` app and redefine them to your liking.

Redesigning templates
^^^^^^^^^^^^^^^^^^^^^

Django uses its own template system (the ``DjangoTemplates`` backend),
which is recommended.

The default webwhois templates are written in the *Django template language*,
which allows separation of templates into several files, their inclusion, and
inheritance, among other features.

If you want to reorganize how information is presented or to add custom site
components, you can override only the components necessary.

For example:

Let us say that you want a different representation of the list of registrars:
a simple list instead of a table. You only need to override the template component
that defines the table (block ``webwhois_content``), which originates in the template
``webwhois/registrar_list.html``.

* Create a file such as :file:`/path/to/my-templates/webwhois/my_registrar_list.html`
  with the following content:

  .. code-block:: django
     :caption: Django: Overriding a template block

     {# Name the template to be extended. #}
     {% extends "webwhois/registrar_list.html" %}

     {# Load library with webwhois filters (allows the use of "add_scheme" filter below). #}
     {% load webwhois_filters %}

     {# Name the block to override. #}
     {% block webwhois_content %}
        {# Your own definition of the block follows. #}
        <ul>
           {% for item in registrars|dictsort:"registrar.name" %}
              <li><a href="{{ item.registrar.url|add_scheme }}">{{ item.registrar.name }}</a></li>
           {% endfor %}
        </ul>
     {% endblock webwhois_content %}

     {# The rest of the template is inherited from the template being extended. #}

* Define the ``template_name`` variable for the corresponding view
  in your URLs module:

  .. code-block:: python
     :caption: Django: Reconfiguring a template for a view

     urlpatterns = [
      # From the template reference, we know that the list is rendered by this view
      # so we tell it that we want to use another template than the default
      url(r'^registrars/$', RegistrarListView.as_view(template_name="webwhois/my_registrar_list.html"), name='registrars'),
      # ...
      # Include the original webwhois URLs
      url(r'^', include('webwhois.urls')
     ]




* Then add the directory path of the custom template
  to the ``DIRS`` list in templates configuration as follows:

  .. code-block:: python
     :caption: Django: Setting a custom template path in project settings

     TEMPLATES = [
         {
             'BACKEND': 'django.template.backends.django.DjangoTemplates',
             # ...
             'DIRS': [
                '/path/to/my-templates',
             ],
         },
     ]

For more about Django templates in fred-webwhois see :doc:`WebwhoisTemplates`.

See also `Django 1.11: Templates
<https://docs.djangoproject.com/en/1.11/topics/templates/>`_ (a brief introduction).

Creating a new localization
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Django uses **gettext** for internationalization and localization.

To make your own localization, `create language files
<https://docs.djangoproject.com/en/1.11/topics/i18n/translation/#localization-how-to-create-language-files>`_,
into which you will place your translations.

Before deployment, remember to `compile the language files
<https://docs.djangoproject.com/en/1.11/ref/django-admin/#django-admin-compilemessages>`_.

See also `Django 1.11: Iternationalization and localization
<https://docs.djangoproject.com/en/1.11/topics/i18n/>`_.

.. todo:: Customizing webwhois views (extending contexts)
   :class: todo-backlog

.. toctree::
   :caption: Reference
   :maxdepth: 1

   WebwhoisTemplates

..   WebwhoisViews
