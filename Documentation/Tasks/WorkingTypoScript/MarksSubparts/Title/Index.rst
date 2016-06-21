.. include:: ../../../../Includes.txt


.. _configure-title:

TITLE mark
~~~~~~~~~~

We are nearly done. Let's recap our progress so far:

- we installed the tutorial's corresponding distribution, thus creating
  a page structure and copying resource files in an appropriate place.

- we have modified an HTML template file by adding subparts and marks for everything,
  which should be output dynamically by TYPO3 CMS.

- we have created a TypoScript template which loads the HTML template file

- in that template, we have created rendering definitions for most of the
  marks and subparts.

We will now configure the TITLE mark. This mark is placed above the middle column
and should output the page title of each page (i.e. the title of the current page).
So we need a content object, which can output a text and this text should come from the database.
Maybe you already have a clue where we are heading.

Let's start by defining a simple :code:`TEXT` object:

.. code-block:: typoscript

	TITLE = TEXT

You should remember that a :code:`TEXT` object has :code:`stdWrap` capabilities.
One of the things :code:`stdWrap` can do is access data about the current page.
Indeed each page in TYPO3 CMS corresponds to a record in the database. The data
related to the current page is loaded into memory and is accessible via the
:ref:`field <t3tsref:stdwrap-field>` property of :code:`stdWrap`.

.. note::

   The above is true because the template is working at page-level.
   When rendering content elements, it will be each content element's
   data that can be accessed using the :code:`field` property.

The title of a page is stored in the database in a column called "title".
So we can add to our TypoScript:

.. code-block:: typoscript

	TITLE = TEXT
	TITLE.field = title

And that is all. Now the TITLE mark gets replaced with the headline of the page.
Again here is the commented and indented code:

.. code-block:: typoscript

	////////////////////////////////////////////////////////////////////////////////////////////
	//
	// Mark TITLE
	//
	////////////////////////////////////////////////////////////////////////////////////////////

	// The mark TITLE outputs the page headline
	TITLE = TEXT
	TITLE.field = title

Now let us define the CONTENTMIDDLE subpart.
