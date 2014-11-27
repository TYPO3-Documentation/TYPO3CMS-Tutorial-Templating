.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../../Includes.txt


.. _configure-title:

TITLE mark
~~~~~~~~~~

We are nearly done. Let's again have a look at what we have done already:
first we have created a page structure in the TYPO3 CMS Backend.
With our current definitions TYPO3 CMS can already display parts of these pages
(namely the menus and the content of the right column). We have modified
an HTML template file by adding subparts and marks for everything,
which should be output dynamically by TYPO3 CMS. Again in the TYPO3 CMS Backend
we have created a template record in the root page. Inside that template record
we have loaded our HTML template and configured most of the marks and subparts.
The marks and subparts, which we have configured, already show their content.
Currently only the mark TITLE and the subpart CONTENTMIDDLE are missing,
then we have basically finished setting up our site. Only a few small things should still be done then.

Now we will configure the mark TITLE. This mark is placed above the middle column
and should output the page title of each page (meaning always the title of the current page).
So we need a cObject, which can output a text and this text should come from the database.
Maybe you already have a clue where the journey is going.

Let's start by defining a simple TEXT object:

.. code-block:: typoscript

	TITLE = TEXT

You should remember that each cObject has stdWrap available in a property "stdWrap". By the way: You should already know that TYPO3 uses a database to store your pages and your page content. Do you know how a database is structured? It contains several tables (e.g. the pages are stored in the table called "pages") and in each table there are fields (e.g. in the table "pages" there is the field "author", which can contain the name of the author of each page. But that just for your information.

So now let's look through the possibilities of stdWrap to check, how it can help us. You will find that stdWrap has the property "field". This property returns the contents of that field of the current page out of the database, which you set as value for the property. You don't have to look into the table "pages" of your database and view its structure to see where TYPO3 stores the page titles. I will tell you: They are in the field called "title".

So we can add to our TypoScript:

.. code-block:: typoscript

	TITLE = TEXT
	TITLE.stdWrap.field = title

And that is all. Now the mark TITLE gets replaced with the headline of the page.
Again here is the commented and indented code:

.. code-block:: typoscript

	##############################################
	#
	# Mark TITLE
	#
	##############################################

	# The mark TITLE outputs the page headline
	TITLE = TEXT
	TITLE.stdWrap.field = title

Now let us define the subpart CONTENTMIDDLE.
