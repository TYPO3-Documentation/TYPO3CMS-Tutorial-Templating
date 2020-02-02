.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _next-steps:

Next steps
""""""""""

.. note::

   There are other possible tasks such as: adding a second level to navigation, creating a graphical menu (without text),
   ensuring that the HTML output conforms to the W3C standard, etc.

In this tutorial we built the website by adding marks and
subparts to an HTML file and mapping them to a TypoScript template,
which is a very common way to do templating in TYPO3 CMS.

There are other possibilities (which might be covered in future tutorials):

- using the TYPO3 extension `automaketemplate: <http://typo3.org/extensions/repository/view/automaketemplate>`_,
  which basically works the same way we learned in this tutorial
  but which automatically wraps up those sections of an HTML page
  which have certain classes or ids in corresponding template subparts.

- using the TYPO3 extension `TemplaVoila! <http://typo3.org/extensions/repository/view/templavoila>`_
  which allows the creation of more flexible page structures.

- using only TypoScript, without any HTML template, for building the website .

- using the Fluid templating engine by applying the FLUIDTEMPLATE
  object rather than the TEMPLATE object.

Do you want to know more about how copying objects in TypoScript works?
Do you know that you can also create so-called "references" instead of copying an object?
If you want to know more about the syntax of TypoScript, have a look at the chapter
:ref:`t3coreapi:typoscript-syntax-start` in "TYPO3 Explained".
