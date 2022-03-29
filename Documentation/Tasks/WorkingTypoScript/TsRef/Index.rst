.. include:: /Includes.rst.txt


.. _how-to-use:

How to use TSref
****************

Before start writing our own TypoScript, let us have a look at what
is already there:

.. code-block:: typoscript

    # Default PAGE object:
    page = PAGE
    page.10 = TEXT
    page.10.value = HELLO WORLD!

If this looks totally weird to you, please read the
:doc:`TypoScript in 45 Minutes Tutorial <t3ts45:Index>` and come back here.
The concepts will be briefly explained again here, but not in as much depth.

Don't forget that the :doc:`TypoScript Reference <t3tsref:Index>` (TSref) is the
ultimate reference in all matters related to TypoScript.

So what do we have by default in our new template:

- Lines starting with :code:`#` are comments. They are not rendered in any way.

- In the next line the object :code:`page` is defined and set to the value :code:`PAGE`.
  This value refers to a :ref:`page object <t3tsref:page>`, which is used to define
  the rendering of a web site page.

- The TSref lists the many properties of the :code:`PAGE` object.
  Among others it accepts a list of content objects represented as a numbered
  array. In the code above :code:`page.10` is the first such content object
  (also called a "cObject" in TypoScript jargon).

  .. note::

     A "cObject" or "content object" is not a "content element". A "content element" is an element,
     which is displayed on a single page in the website. Content elements can be edited in the Page module.

  Again the :ref:`TypoScript Reference <t3tsref:cobjects>` will give you an overview
  of all available content object types. In our current template, we use a simple
  :code:`TEXT` object.

- The :code:`TEXT` object itself has several properties, including one called
  :code:`value` which is used to set the text itself.
  Here it is set to "HELLO WORLD!"

These lines are enough to create an output in the frontend, albeit very crude.
Just view any page in the web site and you should see the following:

.. figure:: ../../../Images/TemplateOutput.png
   :alt: The template output in the frontend
