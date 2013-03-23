.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _next-steps:

Next steps
""""""""""

.. note::
   What might be the next task? E.g. adding a second level for the navigation.
   Create no text menu, but a graphical menu. Ensure that HTML-output is conform to W3C-standard, etc.

In this tutorial we built the website by adding markers and
subparts to a HTML file and mapping them to a TypoScript template,
which is a very common way to do the job.

There are other possibilities (which might be covered in future tutorials):

- using the TYPO3 extension `automaketemplate: <http://typo3.org/extensions/repository/view/automaketemplate>`_,
  which basically works the same way as we do in this tutorial,
  but which automatically wraps those sections of a HTML page,
  which have a certain class or id, in corresponding template subparts.

- using the TYPO3 extension `TemplaVoila! <http://typo3.org/extensions/repository/view/templavoila>`_
  which allows to create more flexible page structures.

- it's also possible to work without any HTML template and build the website only with
  Typoscript

- in more recent versions of TYPO3 CMS, it is also possible to use a FLUIDTEMPLATE
  object rather than a TEMPLATE object, and thus make use of the Fluid templating
  engin.

Do you want to know more about how copying objects in TypoScript works?
Do you know that you can also create so called "references" instead of copying an object?
If you want to know more, have a look at the manual :ref:`t3tssyntax:start`!
